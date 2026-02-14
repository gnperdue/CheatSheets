
## Get MongoDB running (assuming installed with Homebrew at v7)

```bash
brew services start mongodb-community@7.0
brew services list
```

## Restart it

```bash
brew services restart mongodb-community@7.0
```

## Stop it

```bash
brew services stop mongodb-community@7.0
```

## Brew services help -- covers all the `brew services` stuff here and more.

```bash
brew services --help
```

## Version

```bash
mongosh --eval "db.version()"
```

## Debugging Empty Report

To check why the report is empty, inspect the MongoDB failures collection:

1. Open your terminal.
2. Run `mongosh` (or accessing your DB UI).
3. Connect to the database: `use moderation_analysis`
4. Check for failures: `db.failures.countDocuments({})`
5. View a failure: `db.failures.findOne()`
6. If `db.failures` is empty, check `db.results`: `db.results.countDocuments({})`. If both are empty, the script is likely not finding any files to process (check paths).