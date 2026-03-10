**问题：**
``` mysql
为什么这两个效率差很多
EXPLAIN SELECT * FROM work_order WHERE code = '6155'; 
EXPLAIN SELECT * FROM work_order WHERE code = 6155;
```

排查思路：
explain慢查询
`system` > `const` > `eq_ref` > `ref` > `range` > `index` > `ALL`

SHOW INDEX查看索引

