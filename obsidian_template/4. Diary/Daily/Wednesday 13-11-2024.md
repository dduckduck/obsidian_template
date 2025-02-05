---
year: 2024
date: 2024-11-13
week_n: 46
tags:
  - daily_note
mood: 8
gym: 1
---
# 📊 Quick overview 
___
*A snapshot of key data to track how your week is going*

[[4. Diary/Weekly/W46_2024]]

```dataviewjs
const WEEK_PATH = `4. Diary/Weekly/W${dv.current().week_n}_${dv.current().year}`;
const DAILY_PATH = `4. Diary/Daily`;

const getWeeklyStats = () => {
    let finished_count = 0;
    let pending_count = 0;
    let completion_rate = 0;
    let gym_visits = 0;
    let total_mood = 0;
    let mood_entries = 0;
    let total_time = 0; 
    let total_tasks = 0;

    for (let t of dv.pages(`"${WEEK_PATH}"`).file.tasks) {
        if (t.fullyCompleted) {
            finished_count++;
            total_tasks++; 
        } else {
            if (!t.parent) {
                pending_count++;
            }
        }
	    if (t.task_t) {
            total_time += t.task_t; 
        }
    }
    completion_rate = (finished_count + pending_count) > 0 ? finished_count / (finished_count + pending_count) : 0;

    for (let day of dv.pages(`"${DAILY_PATH}"`).where(p => p.week_n == dv.current().week_n && p.year == dv.current().year)) {
        if (day.gym) gym_visits++;
        if (day.mood !== undefined) {
            total_mood += day.mood;
            mood_entries++;
        }
    }

    const average_mood = mood_entries > 0 ? (total_mood / mood_entries).toFixed(2) : "N/A";


    let total_duration = moment.duration(total_time, 'milliseconds');
    let formatted_total_time = `${total_duration.hours()} hours and ${total_duration.minutes()} minutes`;


    let average_time_per_task = total_tasks > 0 ? total_time / total_tasks : 0;
    let formatted_average_time = moment.duration(average_time_per_task, 'milliseconds').humanize();

    return {
        finished_count,
        pending_count,
        completion_rate,
        gym_visits,
        average_mood,
        formatted_total_time,
        formatted_average_time
    };
};

const weeklyStats = getWeeklyStats();


dv.table(
    ["Metric", "Value"],  
    [
        ["Tasks Finished", weeklyStats.finished_count],
        ["Tasks Pending", weeklyStats.pending_count],
        ["Task Completion Rate", `${(weeklyStats.completion_rate * 100).toFixed(2)}%`],
                ["Total Time Spent on Tasks", weeklyStats.formatted_total_time],
        ["Average Time per Task", weeklyStats.formatted_average_time],
        ["Went to Gym", `${weeklyStats.gym_visits} times`],
        ["Average Mood", weeklyStats.average_mood]

    ]
);

```

# 📖 Diary
___
*A space for logging your daily experiences and personal insights.*

Still stuck in VIM. I guess that's my life now... 
