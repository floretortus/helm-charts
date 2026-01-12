## Getting started

To properly manage your Helm chart and its dependencies,
you will need to configure the Git repository and adjust CI pipeline.

### Git Configuration:

- `Chart.yaml`: To include `hlib` dependency, it is needed to add a dependencies section to this file, for example

    ```yaml
    apiVersion: v2
    description: Helm chart to deploy microservice
    name: Microservice
    version: 1.0.0
    dependencies:
      - name: hlib
        version: <desired_library_version>
        repository: https://github.com/anatolek/hlib
    ```

- `.helmignore`: It is important to exclude unnecessary files and directories from your chart package.
  Add it to the helm chart folder.

  ```text
  # Patterns to ignore when building packages.
  # This supports shell glob matching, relative path matching, and
  # negation (prefixed with !). Only one pattern per line.
  .DS_Store
  # Common VCS dirs
  .git/
  .gitignore
  .bzr/
  .bzrignore
  .hg/
  .hgignore
  .svn/
  # Common backup files
  *.swp
  *.bak
  *.tmp
  *.orig
  *~
  # Helm
  .helmignore
  # Various IDEs
  .project
  .idea/
  *.tmproj
  .vscode/
  ```

- `.gitignore`: It is important to include the `charts/` in this file to avoid including unnecessary duplicate content in a git repository.
  This file is usually located in the root of the repository.

  ```text
  # .gitignore
  charts/
  ```

- `Chart.lock`: It locks the versions of the dependencies.
  Run `helm dependency update` to generate this file, and then commit it to your Git repository.

### CI Pipeline Configuration:

Issue the following commands to add the Helm repository that contains the library chart, update dependencies, and push chart artifact:

```shell
helm lint <helm_chart_location>  # optionally
helm repo add hlib https://github.com/anatolek/hlib
helm dependency build <helm_chart_location>
helm package <helm_chart_location>
```

#### `helm dependency` commands explanation

| Command                  | Purpose                                               | Modifies `Chart.lock`? | When to Use                                                                   |
|--------------------------|-------------------------------------------------------|------------------------|-------------------------------------------------------------------------------|
| `helm dependency update` | Resolves and downloads dependencies from `Chart.yaml` | ✅ Yes                  | When you add or change dependencies in `Chart.yaml`                           |
| `helm dependency build`  | Builds the `charts/` directory from `Chart.lock`      | ❌ No                   | When you already have a `Chart.lock` and want to rebuild dependencies exactly |

### Template Usage

After all the settings are done, you can start using the basic templates, variables, and helper functions defined in the GT library.
Some examples are described in the `examples/` folder.
