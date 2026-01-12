## Contributions

### Versioning rules

Code version contains three positions `X.Y.Z`

`Z` - should be increased **for fixes**

`Y` - should be increased for code update with **adding new features**

`X` - should be increased if update **breaks backward compatibility**

### Documentation-related changes

*README.md* files are generated using a [helm-docs](https://github.com/norwoodj/helm-docs/tree/master) utility.
Don't try to add changes directly.

```shell
helm-docs --skip-version-footer
```

- Add documentation on variables to `values.yaml`
- A new section should be added as a separate file to `.docs/`, and then linked into the template `README.md.gotmpl`.
