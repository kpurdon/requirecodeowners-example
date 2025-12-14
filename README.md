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
    No subdirectories found at level 1. Add subdirectories or set level to 0 in .requirecodeowners.yml.
  ✗ nonexistent
    Directory not found. Create it or remove from .requirecodeowners.yml.
  ✗ services/also-uncovered
    Not covered by CODEOWNERS. Add: /services/also-uncovered/ @your-team
  ✗ services/uncovered
    Not covered by CODEOWNERS. Add: /services/uncovered/ @your-team

✗ 4 directories failed CODEOWNERS check
```

GitHub Actions also shows a summary table with all errors.
