# requirecodeowners-example

Example usage of [kpurdon/requirecodeowners](https://github.com/kpurdon/requirecodeowners).

## Structure

```
services/
  foo/    # requires CODEOWNERS entry (level: 1)
  bar/    # requires CODEOWNERS entry (level: 1)
libs/     # requires CODEOWNERS entry (level: 0)
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

## Workflow

Runs on all PRs and pushes to main.
