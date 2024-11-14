---
year: {{date:YYYY}}
date: {{date}}
week_n: {{date:W}} 
tags:
  - weekly_note
---

# 🗓️ Week 
___
*Diary*
```dataview
TABLE file.mtime as "Last modified"
FROM "4. Diary/Daily"
WHERE week_n = this.week_n and year = this.year
SORT date ASC
```


# 📋Tasks
___
*List of tasks for this week*



```dataviewjs

let total_time = 0;

for (let v of dv.current().file.tasks){
	if(v.task_t && v.fullyCompleted){
		total_time+=v.task_t;
	}
}

let duration = moment.duration(total_time, 'milliseconds'); 
let formatted_duration = `${duration.hours()} hours and ${duration.minutes()} minutes`; 
dv.paragraph("**Time spent on tasks:** " + formatted_duration);
```

# ⚠️ Overdue
___
*List of unfinished tasks*
```dataview
TASK 
from "4. Diary/Weekly"
where due and due < file.cday and !fullyCompleted and file.name != this.file.name
sort file.cday asc
```





