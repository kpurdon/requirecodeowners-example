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

```
validation failed:
  - no CODEOWNERS entry covers: services/also-uncovered
  - no CODEOWNERS entry covers: services/uncovered
  - directory does not exist: nonexistent
  - no subdirectories found at level 1 in: empty
```
