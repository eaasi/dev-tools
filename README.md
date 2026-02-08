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

## License

This repository and its content are distributed under the [Apache-2.0](./LICENSE) license.

Copyright (c) 2025 Yale University (unless otherwise noted).
