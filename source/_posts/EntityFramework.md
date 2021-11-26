---
title: Entity Framework
date: 2021-11-10 09:48:05
tags: 学无止境
---

## 查询语句
``` C++
动态条件查询
var item = db.pmsheets.ToList();
    if (!string.IsNullOrEmpty(department))
        item = item.Where(e => e.department == department).ToList();
    if (!string.IsNullOrEmpty(project))
        item = item.Where(e => e.project == project).ToList();
    var items = item.Select(e => new {
        paras = e.station
    }).Distinct().ToList();

```

