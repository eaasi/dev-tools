# EAASI DevTools

This repository contains a collection of reusable configs, tasks and workflows for bootstrapping EAASI-specific development environments.

## Getting Started

This project uses [mise](https://github.com/jdx/mise) for managing development tools, environment variables and tasks.
Detailed installation instructions can be found in its official [documentation](https://mise.jdx.dev/installing-mise.html).

Once installed, mise should be activated in the current shell session by following [instructions](https://mise.jdx.dev/installing-mise.html#shells) for your specific shell.

> [!TIP]
> Optionally, autocompletion for your shell can be set up as documented [here](https://mise.jdx.dev/installing-mise.html#autocompletion).
> Besides the `mise` CLI itself, this will also enable autocompletion for all project-specific tasks.

For an overview of all available tasks and their parameters, take a look at the provided [config](./.config/mise) or simply run:

```shell
mise tasks ls
```

> [!NOTE]
> Running any task should automatically install all required development tools as needed (see [docs](https://mise.jdx.dev/dev-tools/#auto-install-mechanisms)).
> For direct use outside of tasks, these tools can also be installed explicitly by executing:
>
> ```shell
> mise install
> ```

### Using Templates

The provided configuration templates are managed with [cargo-generate](https://github.com/cargo-generate/cargo-generate), which will be installed by mise automatically.

> [!WARNING]
> By default, cargo-generate assumes an empty target directory when applying rendered templates and will fail if any conflicts are found, but it can also be instructed to overwrite all existing files during the generation process.

To apply a specific template to a target repository, execute the following task:

```shell
mise run generate <target-repo-dir> <template-dir>
```

To see an overview of all available templates and choose one interactively, simply run:

```shell
mise run generate <target-repo-dir>
```

For more advanced use cases, the `cargo-generate` binary should be called directly:

```shell
cargo-generate generate --init --name "dev-tools" \
  --path <dev-tools-repo-dir> --destination <target-repo-dir>
```

> [!TIP]
> To simplify maintenance and enable the updating of previously generated (and possibly modified) configuration templates, the following procedure can be used:
>
> 1. Prepare a dedicated Git branch (e.g. named `build/dev-tools-base`) in the target repository:
>
>    ```shell
>    mise run prepare -b "build/dev-tools-base" <target-repo-dir>
>    ```
>
>    This step checks out and prepares an existing branch or creates an empty orphan-branch in the target repository.
>
> 1. Apply each configuration template to the target repository (e.g. by running `mise run generate`).
> 1. Commit all relevant changes to the base branch (in batch or each change individually) using Git.
> 1. Merge the updated base branch into the target branch (e.g. `main`) using the following commands:
>
>    ```shell
>    # switch to a target branch...
>    git switch main
>    # when merging for the first time...
>    git merge "build/dev-tools-base" --allow-unrelated-histories
>    # for all subsequent merges...
>    git merge "build/dev-tools-base"
>    ```
>
>    Potential merge conflicts can then be resolved using the Git-native 3-way merge (see [docs](https://git-scm.com/docs/merge-strategies) for more details).

## License

This repository and its content are distributed under the [Apache-2.0](./LICENSE) license.

Copyright (c) 2025 Yale University (unless otherwise noted).
