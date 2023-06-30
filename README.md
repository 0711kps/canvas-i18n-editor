# Canvas I18n Editor
A cli tool for canvas-lms self hoster with ability to modify i18n  

## Features
- [x] update i18n by argument used by I18n.t
- [ ] compare and remove unused i18n content for you
- [ ] update i18n by the content
## TODO
- [ ] support custom locale
- [ ] support array content
- [ ] support updating i18n with multiline content(althrough multiline i18n doesn't seems to work in most of the pages)

## Prerequisite

- a canvas-lms project with environments setup
- js i18n index files generated
- i18n yml template generated(optional, if you want to clean the unused content)

## Usage
Canvas use two types of translation keys, one from rails, and another from gem "i18nliner", and there's an extra workflow to generate frontend i18n content  
this tool help you change them quickly.  

#### change exist or add new translation content

```bash
# liner style key
canvas-i18n-editor 'Dashboard' '控制台'
# rails style key
canvas-i18n-editor 'account_settings.user' '用戶'
```
it will find the correctly key, and update the locales file  

⚠ notice that the rails style key always followed by a "scope", e.g. "account_settings" in above example  

⚠ in rails files, the scope will be the folder structure inside `app/views/`  
⚠  e.g. `eat.apple` argument used in `app/views/layouts/_fixed_bottom.html.erb` should be `layouts.fixed_bottom.eat.apple` in cli tool  

⚠ in frontend, the scope can be found in the first few lines, there will be one line like this `useI18nScope('...')`  
⚠ e.g. `titles.assignment_rubric_details` argument in `ui/features/discussion_topic/jquery/assignmentRubricDialog.js` should be `assignmentRubricDialog.titles.assignment_rubric_details` in cli tool  


#### add new translation content

```bash
canvas-i18n-editor 'Happy Birthday!' '生日快樂！'
```

this generate new key, and update locales file for you  

```yml
       student_graph_title: 學習活動紀錄
       page_view_label: 網頁點閱數
       participation_label: 課程參與
+  happy_birthday_41745fd9: 生日快樂！
```

⚠️ notice: if the content is used in frontend, make sure to regenerate the i18n index files with `bundle exec rails i18n:generate_js`  
