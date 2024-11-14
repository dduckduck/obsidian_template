
# 😌 Mood
```dataviewjs 
const hue1 = 13 // red
const hue2 = 132 // green

const calendarData = {
    year: 2024, // optional, remove this line to autoswitch year 
    intensityScaleStart: 0,
    intensityScaleEnd: 10,
    colors: {
        red2green: [
            `hsl(${hue1}, 100%, 37%)`,     // 1 - darkest red
            `hsl(${hue1}, 100%, 50%)`,     // 2 - 
            `hsl(${hue1}, 100%, 60%)`,     // 3 - 
            `hsl(${hue1}, 100%, 77%)`,     // 4 - lightest red
            `hsl(0, 0%, 80%)`,             // 5 - neutral gray
            `hsl(${hue2*0.7}, 70%, 72%)`,  // 6 - lightest green
            `hsl(${hue2*0.85}, 43%, 56%)`, // 7 - 
            `hsl(${hue2}, 49%, 36%)`,      // 8 - 
            `hsl(${hue2}, 59%, 24%)`,      // 9 - darkest green
        ],
    },
    entries: []
}


function formatDate(dateTime) { const year = dateTime.year; const month = String(dateTime.month).padStart(2, '0'); 
const day = String(dateTime.day).padStart(2, '0');
return `${year}-${month}-${day}`;
}

for (let page of dv.pages('"4. Diary/Daily"').where(p => p.mood)) { 
    const formattedDate = formatDate(page.date);
    calendarData.entries.push({
        date: formattedDate, 
        intensity: page.mood,
        content: await dv.span(`[[${page.file.name}|]]`),
    });
}
renderHeatmapCalendar(this.container, calendarData);

```

# 🏋️ Gym

```dataviewjs 
const calendarData = {
    entries: []
}
function formatDate(dateTime) { const year = dateTime.year; const month = String(dateTime.month).padStart(2, '0'); 
const day = String(dateTime.day).padStart(2, '0');
return `${year}-${month}-${day}`;
}

for (let page of dv.pages('"4. Diary/Daily"').where(p => p.gym)) { 
    const formattedDate = formatDate(page.date);
    calendarData.entries.push({
        date: formattedDate, // in github docs: YYYY-MM-DD
        intensity: page.mood,
        //content: await dv.span(`[](${page.file.name})`), // for hover preview
    });
}
renderHeatmapCalendar(this.container, calendarData);

```
