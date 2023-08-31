---
banner: "https://fastly.jsdelivr.net/gh/luxiaogen/images@master/2023/J20.jpeg"
banner_icon: 🔥
banner_x: 0.5
banner_y: 0.41
---
```dataviewjs
let setting = {};

//在和风天气中创建的 Api key
setting.key = "c7ecf937506649929b43a171dcbee513";

setting.city = "无锡";//城市名
setting.days = 7;//天气预报天数
setting.headerLevel = 2;//添加标题的等级
setting.addDesc = true;//是否添加描述
setting.onlyToday = false;//是否只在当天显示
setting.anotherCity = "";//添加另外一个城市

//脚本文件 weatherView.js 所在路径
dv.view("template/script/weatherView",setting)
```
## 倒计时、每日一句
```ad-flex
%%notice1%%
> [!stickies3]
> #### 倒计时
>> 今年已过去 <%+* tR+= moment().diff(tp.date.now("YYYY-1-1"), "days") %> 天
>> 
>> 距春节还有<%+* let edate = moment("2022-02-01", "yyyy-MM-DD"); let from = moment().startOf('day'); edate.diff(from, "days") >= 0 ? tR += edate.diff(from, "days") : tR += edate.add(1, "year").diff(from, "days") %> 天

%%notice2%%
> [!stickies3|blue]
>```dataviewjs
async function removeMarkdown (text) {
let excludeComments= true;
let excludeCode= true; 
let plaintext = text;
if (excludeComments) {plaintext = plaintext.replace(/<!--.*?-->/sg, "").replace(/%%.*?%%/sg, "");}
if (excludeCode) {plaintext = plaintext.replace(/```([\s\S]*)```[\s]*/g, "");}plaintext = plaintext.replace(/`\$?=[^`]+`/g, "").replace(/^---\n.*?\n---\n/s, "").replace(/!?\[(.+)\]\(.+\)/g, "$1").replace(/\*|_|\[\[|\]\]|\||==|~~|---|#|> |`/g, ""); return plaintext;}
async function getradomnote (files) {
const random = Math.floor(Math.random() * (files.length - 1));
const randomNote = files[random];
dv.paragraph(randomNote.link);
const sampleTFile = app.vault.getAbstractFileByPath(randomNote.path);
const contents = await app.vault.cachedRead(sampleTFile); 
return contents;}
let reg=/[\u4e00-\u9fa5]/
let nofold = '!"88-Template" and !"99-Attachment" and !"50-Inbox" and !"20-Diary"';
let files = dv.pages(nofold).file;
let content =await getradomnote(files);
let clean= await removeMarkdown(content);
let lines = clean?.split("\n").filter(line => line.match(reg));
const randomline = Math.floor(Math.random() * (lines.length - 1));
lines = lines[randomline]?.replace(/(\r|\n|#|-|\*|\t|\>)/gi,"").substr(0,80) + '...';
dv.span(lines);
>```

%%notice3%%
> [!stickies3|pink]
> #### 每日一句
> ```dataviewjs
 let history = Object.assign(JSON.parse(await app.vault.adapter.read(".obsidian/.diary-stats")));
 let today = moment().format("YYYY-MM-DD");
 if (history.hasOwnProperty(today))
 {
 let quotes=history[today].quotes;
 dv.el("blockquote", quotes);
 }
> ```

%%notice4%%
> [!stickies3|green]
> ### 💌
> 开启美好的一天
```


## moc导航
````ad-flex
```ad-note
title: 🤔 快速导航
color: 178,155,64
> “Quick Access”
- 📆 `$= '[[日记统计#'+ moment().format("YYYY-MM") +'|当月日记]]'`

```

```ad-note
title: 🤩 主页
color: 139,65,06
> “Tutorials”

- 🚩 [luxiaogen的B站](https://space.bilibili.com/66612226?spm_id_from=333.999.0.0)

```
````





## 最近编辑
```dataview
table WITHOUT ID file.link AS "标题",file.mtime as "时间"
from !"10 归档" and !"1 看板"
sort file.mtime desc
limit 5
```
## 三天内创建的笔记
```dataview
table file.ctime as 创建时间
from ""
where date(today) - file.ctime <=dur(3 days)
sort file.ctime desc
limit 5
```
```dataview
TABLE WITHOUT ID
    rows.file[0].cday.year + "年 " + rows.file[0].cday.month + "月" AS "月份",length(rows) + " 篇" AS "数量"
    where !contains(file.folder, "Template") and !contains(file.folder, "1 看板")
   GROUP BY file.cday.year + "年 " + file.cday.month + "月" AS "Group"
   SORT rows.file[0].cday DESC
```











































