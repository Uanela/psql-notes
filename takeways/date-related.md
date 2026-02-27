# Date Related Takeways

## Extract a certain part of Date

```sql
SELECT EXTRACT(MONTH FROM "createdAt") FROM "Users"
SELECT EXTRACT(DAY FROM "createdAt") FROM "Users"
SELECT EXTRACT(HOUR FROM "createdAt") FROM "Users"
SELECT EXTRACT(MINUTE FROM "createdAt") FROM "Users"  
SELECT EXTRACT(SECOND FROM "createdAt") FROM "Users" 
SELECT EXTRACT(EPOCH FROM "createdAt") FROM "Users" -- total time in seconds 
```

## Group Rows By Time Intervals

To achive it use `DATE_TRUNC` which is a time bucketing function and falls into the category of `non-aggregation functions` which operates kind of as an normal field.

```sql
SELECT COUNT(*) as count, DATE_TRUNC('day', user."createdAt") as "timeBucket"
FROM "Users" user
GROUP BY "timeBucket"
```
