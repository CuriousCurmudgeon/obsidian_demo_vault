---
date: 2023-01-06
tag: weekly_summary
---

```dataviewjs
const currentWeekNumber = dv.current().date.weekNumber;
const vibesByDay = dv
	.pages('"Work" and #daily_note')
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
	.pages('"Work" and #daily_note')
	.where(n => n.date.weekNumber == currentWeekNumber)
	.sort(n => n.date)
	.file.link)
```

# Meetings
```dataviewjs
let currentWeekNumber = dv.current().date.weekNumber;
dv.list(dv
	.pages('"Work" and #meeting')
	.where(n => n.date.weekNumber == currentWeekNumber)
	.sort(n => n.date)
	.file.link)
```

# Issues
```dataviewjs
let currentWeekNumber = dv.current().date.weekNumber;
dv.table(["Link", "Start Date", "Finish Date"], dv
	.pages('"Work" and #issue')
	.where(n => currentWeekNumber >= n.start_date.weekNumber)
	.where(n => !n.finish_date || currentWeekNumber <= n.finish_date.weekNumber)
	.sort(n => [n.start_date, n.finish_date])
	.map(n => [n.file.link, n.start_date, n.finish_date]))
```

# Other
```dataviewjs
let currentWeekNumber = dv.current().date.weekNumber;
dv.list(dv
	.pages('"Work" and !#issue and !#meeting and !#daily_note and !#weekly_summary')
	.where(n => n.date && n.date.weekNumber == currentWeekNumber)
	.sort(n => n.date)
	.file.link)
```

# Thoughts
*Unstructured writeup about how I thought the week went*