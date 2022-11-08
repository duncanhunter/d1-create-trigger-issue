# d1 CREATE TRIGGER issue reproduction

## Steps to reproduce

### With SQLite full test search (fts)

#### 1. Create and seed d1 with trigger fails 

```
npx wrangler d1 create foods

npx wrangler d1 execute foods --file=./test-with-fts/dump.sql
```

#### 2. Comment out trigger in ./test-with-fts/dump.sql and re seed and it passes

- Comment out the trigger code shown below
```
-- CREATE TRIGGER foods_ai AFTER INSERT ON foods BEGIN INSERT INTO foods_fts (rowid, name, foodId) VALUES (new.id, new.name, new.foodId); END;

```

- Run wrangler to seed the db

```
npx wrangler d1 execute foods --file=./test-with-fts/dump.sql
```

### Without SQLite full test search (fts)

Run the same steps as above but with test-without-fts files (note the different file and db names) which will show the same failure on the CREATE TRIGGER command in the above steps with fts. Same success when CREATE TRIGGER is commented out.
