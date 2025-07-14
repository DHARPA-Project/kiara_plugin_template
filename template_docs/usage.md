# `kiara_plugin.template` features and how to use them

Note: all paths are relative to the project root folder, and commands should be executed there (unless otherwise specified), `PLUGIN_NAME` is used as a stand-in for the actual name you chose when creating your project


## How to...

### ...add a new Python dependency

```
uv add PACKAGE_NAME
```

### ...add a new cli sub-command

`kiara` uses [`click`](https://click.palletsprojects.com/en/stable/) to parse the user command-line arguments. Check
out their documentation to learn how to create commands and command-groups in detail.

#### Implement the commands/command-groups

Create a new (folder-based) Python module:

```
src/kiara_plugin/PLUGIN_NAME/interfaces/cli/__init__.py
```

Pick a name for your sub-command (we'll use `cmd_example` here), and create a child-module with that name:

```
src/kiara_plugin/PLUGIN_NAME/interfaces/cli/cmd_example.py
```

Then use code like the following to implement your cli sub-commands:

```python
import rich_click as click

@click.group("cmd-example")
@click.pass_context
def cmd_example_group(ctx: click.Context):
    """Here goes a short description what the command group does."""

@cmd_example_group.command("print-hello-world")
@click.pass_context
def print_hello_world(ctx: click.Context):
    """Here goes a short description what the command does."""

    print("Hello World!")
```

#### Register the commands/command-groups

Now, in `pyproject.toml`, find or create a sub-section named `[project.entry-points."kiara.cli_subcommands"]` and configure it like so:

```toml
[project.entry-points."kiara.cli_subcommands"]
dev-example = "kiara_plugin.PLUGIN_NAME.interfaces.cli.cmd_example:cmd_example_group"
```

