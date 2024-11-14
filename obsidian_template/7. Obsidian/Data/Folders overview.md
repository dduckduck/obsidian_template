# 📁 Folders 
```dataviewjs
dv.table(["Folder","Entries"],[
["Raw notes",dv.pages('"2. Raw notes"').length],
["Daily notes",dv.pages("#daily_note").length-1],
["Weekly notes",dv.pages("#weekly_note").length-1],
["Topics",dv.pages('"3. Topics"').length]
].sort((a,b)=>b[1]-a[1]));
```
