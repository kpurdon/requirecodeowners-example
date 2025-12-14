# requirecodeowners-example

Example usage of [kpurdon/requirecodeowners](https://github.com/kpurdon/requirecodeowners).

## Structure

```
services/
  foo/    # requires CODEOWNERS entry
  bar/    # requires CODEOWNERS entry
```

## Configuration

`.requirecodeowners.yml` requires each subdirectory under `services/` to have a CODEOWNERS entry:

```yaml
directories:
  - path: services
    level: 1
```

## Workflow

The action runs on PRs that modify CODEOWNERS or service directories.
