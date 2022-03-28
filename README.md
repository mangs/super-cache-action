# `mangs/dependency-super-cache-action`

GitHub Action that is simple and greatly improves `node_modules` cache performance over `actions/cache`'s default recommendations

## Simple Example

```yaml
- uses: actions/setup-node@v3
  with:
    node-version: "16.14.2"
- id: super-cache
  uses: mangs/dependency-super-cache-action@v1
- if: steps.super-cache.outputs.cache-hit != 'true'
  run: npm ci
```

## Multiline Dependencies Example

```yaml
- uses: actions/setup-node@v3
  with:
    node-version: "16.14.2"
- id: super-cache
  uses: mangs/dependency-super-cache-action@v1
  with:
    dependencies_to_cache: |
      ./.eslintcache
      ./node_modules
- if: steps.super-cache.outputs.cache-hit != 'true'
  run: npm ci
```

## Action Inputs

| Name                    | Required | Default Value    | Descripition                                                                                |
| ----------------------- | -------- | ---------------- | ------------------------------------------------------------------------------------------- |
| `dependencies_to_cache` | N        | `./node_modules` | Single- or multi-line string wherein each line targets dependencies to cache; can use globs |

## Action Outputs

| Name        | Data Type | Descripition                                                              |
| ----------- | --------- | ------------------------------------------------------------------------- |
| `cache-hit` | Boolean   | A boolean value indicating if a match was found in the repository's cache |
