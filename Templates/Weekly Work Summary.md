---
date: {{date:YYYY-MM-DD}}
tag: weekly_summary
---

```dataviewjs
const currentWeekNumber = dv.current().date.weekNumber;
const vibesByDay = dv
	.pages("#daily_note")
	.where(n => n.date.weekNumber == currentWeekNumber)
	.sort(n => n.date)
	.map(n => [n.date.weekdayShort, n.vibes])
	.values

const chartData = {
	type: "bar",
	data: {
		labels: vibesByDay.map(x => x[0]),
		datasets: [{
			label: "Vibes",
			data: vibesByDay.map(x => x[1]),
			backgroundColor: ['#4bc0c0']
		}]
	},
	options: {
		scales: {
			y: {
				max: 10
			}
		}
	}
}

window.renderChart(chartData, this.container)
```

# Daily Notes
```dataviewjs
let currentWeekNumber = dv.current().date.weekNumber;
dv.list(dv
	.pages("#daily_note")
	.where(n => n.date.weekNumber == currentWeekNumber)
	.sort(n => n.date)
	.file.link)
```

# Meetings
```dataviewjs
let currentWeekNumber = dv.current().date.weekNumber;
dv.list(dv
	.pages("#meeting")
	.where(n => n.date.weekNumber == currentWeekNumber)
	.sort(n => n.date)
	.file.link)
```

# Issues
```dataviewjs
let currentWeekNumber = dv.current().date.weekNumber;
dv.table(["Link", "Start Date", "Finish Date"], dv
	.pages("#issue")
	.where(n => currentWeekNumber >= n.start_date.weekNumber)
	.where(n => !n.finish_date || currentWeekNumber <= n.finish_date.weekNumber)
	.sort(n => [n.start_date, n.finish_date])
	.map(n => [n.file.link, n.start_date, n.finish_date]))
```

# Other
```dataviewjs
let currentWeekNumber = dv.current().date.weekNumber;
dv.list(dv
	.pages('"Notes" and !#issue and !#meeting and !#daily_note and !#weekly_summary')
	.where(n => n.date && n.date.weekNumber == currentWeekNumber)
	.sort(n => n.date)
	.file.link)
```

