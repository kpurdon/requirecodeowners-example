# requirecodeowners-example

Example usage of [kpurdon/requirecodeowners](https://github.com/kpurdon/requirecodeowners).

This example intentionally fails to demonstrate all failure modes.

## Structure

```
services/
  foo/           # ✅ has CODEOWNERS entry
  bar/           # ✅ has CODEOWNERS entry
  uncovered/     # ❌ missing CODEOWNERS entry
  also-uncovered/# ❌ missing CODEOWNERS entry
libs/            # ✅ has CODEOWNERS entry
empty/           # ❌ has no subdirectories (level: 1)
nonexistent/     # ❌ directory does not exist
```

## Configuration

`.requirecodeowners.yml`:

```yaml
directories:
  - path: services
    level: 1
  - path: libs
  - path: nonexistent    # does not exist
  - path: empty
    level: 1             # no subdirectories
```

## CODEOWNERS

```
/services/foo/ @kpurdon
/services/bar/ @kpurdon
/libs/ @kpurdon
```

## Expected Output

Console:
```
  ✗ empty
    no subdirectories at level 1. Create subdirectories or set level: 0
  ✗ nonexistent
    directory does not exist. Create it or remove from .requirecodeowners.yml
  ✗ services/also-uncovered
    missing CODEOWNERS entry. Add to CODEOWNERS: /services/also-uncovered/ @owner
  ✗ services/uncovered
    missing CODEOWNERS entry. Add to CODEOWNERS: /services/uncovered/ @owner

✗ 4 directories failed CODEOWNERS check
```

GitHub Actions also shows a summary table with all errors.
