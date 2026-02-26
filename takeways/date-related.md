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
