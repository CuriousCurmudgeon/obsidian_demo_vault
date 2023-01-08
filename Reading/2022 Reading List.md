```dataviewjs
let bookGroups = dv.pages('#book and "Reading"')
	.where(p => p.start_date.year == 2022 || p.complete_date.year == 2022)
	.groupBy(p => p.genre)

for (let group of bookGroups) {
	dv.header(3, group.key);
	dv.table(["Link", "Name", "Started", "Completed", "Rating"],
		group.rows
			.sort(k => k.rating, 'desc')
			.map(k => [k.file.link, k["title"], k["start_date"], k["complete_date"], k.rating]))
}
```
