# requirecodeowners-example

Example usage of [kpurdon/requirecodeowners](https://github.com/kpurdon/requirecodeowners).

This example intentionally fails to demonstrate the tool's behavior.

## Structure

```
services/
  foo/        # ✅ has CODEOWNERS entry
  bar/        # ✅ has CODEOWNERS entry
  uncovered/  # ❌ missing CODEOWNERS entry
libs/         # ✅ has CODEOWNERS entry
```

## Configuration

`.requirecodeowners.yml`:

```yaml
directories:
  - path: services
    level: 1          # check each subdirectory
  - path: libs        # level 0 (default) checks the directory itself
```

## CODEOWNERS

```
/services/foo/ @kpurdon
/services/bar/ @kpurdon
/libs/ @kpurdon
```

Note: `services/uncovered/` has no CODEOWNERS entry, so validation fails.

## Expected Output

```
validation failed:
  - no CODEOWNERS entry covers: services/uncovered
```
