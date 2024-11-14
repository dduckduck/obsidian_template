
#  📔Diary
```dataviewjs
const MAX_ENTERIES = 7;
const PATHS = { '"4. Diary/Daily"': "Daily", '"4. Diary/Weekly"': "Weekly"};

function getFolderOverview() {
	/*Building entries*/
	const table = { headers: [], rows: [] };
	const tmp = [];
	for(let path in PATHS){
		table.headers.push(PATHS[path]);
		const links = dv.pages(path).sort((p)=>p.date,"desc").slice(0, MAX_ENTERIES).map((page)=>page.file.link);
		tmp.push(links);
	}
	table.rows.push(tmp);
	return table; 
}
function getTaskOverview(){
	const table = {headers:["Not completed", "Completed","Time spent"],rows:[]};
	const tasks = dv.pages("#weekly_note").file.tasks;
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

	table["rows"].push([uncompleted,completed,readableTaskTime]);
	return table;
}


const folderOverview =  getFolderOverview();
const taskOverview = getTaskOverview();

/*Table 1*/
dv.table(folderOverview["headers"],folderOverview["rows"]);


```
# 📥 Latest entries
```dataview
table file.cday as Created, file.tags as Tags
from "3. Topics" or "2. Raw notes"
limit 10
```




