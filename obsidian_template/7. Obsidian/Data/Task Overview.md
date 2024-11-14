
# 📑  Tasks
```dataviewjs
const WEEKLY_PATH = "4. Diary/Weekly";
function taskTime(){
	const table = {headers:["Completed", "Not Completed","Time spent"],rows:[]};
	const tasks = dv.pages(`"${WEEKLY_PATH}"`).file.tasks;
	let completed = 0;
	let uncompleted = 0;
	let taskTime = 0;
	for(let t of tasks){
		if(t.completed){
			completed++;
			if(t.task_t){
			taskTime+=t.task_t;
			}
		}else{
			uncompleted++;
		}
	}
const readableTaskTime = `${Math.floor(taskTime / (1000 * 60 * 60))}h ` + `${Math.floor((taskTime / (1000 * 60)) % 60)}m ` +`${Math.floor((taskTime / 1000) % 60)}s`;

	table["rows"].push([completed,uncompleted,readableTaskTime]);
	return table;
}


function getTaskOverview() {
    const table = { headers: ["Upcoming", "Overdue", "Not assigned"], rows: [] };
    const tasks = dv.pages("#weekly_note").file.tasks;
  const todayDate = new Date().toISOString().split("T")[0];
	const upcoming = [];
	const overdue = [];
	const na = [];
	
    for (let t of tasks) {
       if(!t.fullyCompleted){
        const cleanedText = t.text.replace(/\[.*?::.*?\]/g, "").trim();
	       if (t.due) {
	            const dueDate = t.due.toISODate();
	            if (dueDate >= todayDate) {
	                upcoming.push(cleanedText);
	            } else {
	                overdue.push(cleanedText);
	            }
	        } else {
		        if(!t.fullyCompleted && !t.parent) na.push(cleanedText);
	        }
       }
    }

    table["rows"].push([upcoming, overdue, na]);
    return table;
}

const taskTimeOverview = taskTime();

/* Tabla de resumen */

const taskOverview = getTaskOverview();


dv.table(taskOverview["headers"], taskOverview["rows"]);
dv.table(taskTimeOverview["headers"],taskTimeOverview["rows"]);

```




