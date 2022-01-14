<!---Documatic-section-fixed: top1-start--->
<p align="center">
  <img alt="vscode logo" src="https://github.com/CodeWithSwastik/vscode-ext/blob/main/images/vscode-ext-2.png?raw=true" width='500px'/>
</p>

<p align="center"><a href="https://GitHub.com/CodeWithSwastik/vscode-ext/graphs/commit-activity"><img src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" alt="Maintenance"></a>
<a href="https://pepy.tech/project/vscode-ext"><img src="https://static.pepy.tech/personalized-badge/vscode-ext?period=total&amp;units=international_system&amp;left_color=orange&amp;right_color=brightgreen&amp;left_text=Downloads" alt="Downloads"></a>
<a href="https://pypi.python.org/pypi/vscode-ext/"><img src="https://badge.fury.io/py/vscode-ext.svg" alt="PyPI version"></a>
<a href="https://github.com/psf/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>

## About

Create vscode extensions and color themes with python.

<!---Documatic-section-fixed: top1-end--->
<!---Documatic-section-fixed: top2-start--->

## Why use this?

Why should you use this for building VScode extensions when you can use typescript? Here are some reasons:

- vscode-ext builds the package.json for you! No need to switch between your extension.py and package.json in order to add commands. It also handles adding Activity Bars, Keybinds and Views.
- vscode-ext provides a more pythonic way of creating the extension. Python also has some powerful modules that Javascript doesn't and you can include these with vscode-ext
- vscode-ext extensions work perfectly with vsce and you can publish your extensions just like you would publish any other extension.

<!---Documatic-section-fixed: top2-end--->

## Requirements

* Python version 3.6 and above
are compatible.
* Install requirements with `pip install -r requirements.txt`.
* `vscode-ext` is pip-installable.
Clone the repository
and run `pip install -e .` in top-level directory to install
package locally
* Alternatively, run `pip install vscode-ext` to install from pypi

### Developers

* There are no specific developer requirements
* No unit tests present
* The project uses GitHub Actions for CI/CD.

| Script | Description |
|:------:|:---------|
| `.github/workflows/docs.yml` | Executed on push to branch `main` |

## Quickstart example

Initialize the extension
with a version (SemVer)
and an extension name.

<!---Documatic-section-code: f12313-examples/hello_world.py-1-3--->
```python
import vscode

ext = vscode.Extension(name="firstext", display_name="First Ext", version="0.0.1")

@ext.event
def on_activate():
    return f"The Extension '{ext.name}' has started"
```

Wrap a function in a command decorator to create a command.
The command name
"Hello World"
is automatically generated
from the function name.

<!---Documatic-section-code: f12313-examples/hello_world.py-5-8--->
```python
@ext.command()
def hello_world():
    vscode.window.show_info_message(f"Hello World from {ext.display_name}")
```

Run the python script to build the extension.

<!---Documatic-section-code: f12313-examples/hello_world.py-16-17--->
```python
vscode.build(ext)
```

## Code structure

Source code is 
The source code has a single-depth (flat) structure.

### Code Entrypoints

There are 23 source code objects
in top-level `__main__`/`__init__`.
They are broken down into the following modules:

* [`vscode.types`](#vscodetypespy) has 15 entrypoints
* [`vscode.compiler`](#vscodecompilerpy) has 2 entrypoints
* [`vscode.extension`](#vscodeextensionpy) has 2 entrypoints
* [`vscode.webviews`](#vscodewebviewspy) has 2 entrypoints
* [`vscode.env_methods`](#vscodeenv_methodspy) has 1 entrypoints
* [`vscode.themes`](#vscodethemespy) has 1 entrypoints

### Class structure

The project has classes which are used in multiple functions:

* `vscode.themes.BaseColorSet` is used 1 times
* `vscode.themes.ColorSet` is used 2 times
* `vscode.extension.Extension` is used 1 times
* `vscode.themes.ColorTheme` is used 2 times

The project's class inheritance structure is:

* `vscode.types.Range` has 1 child classes:
  * `vscode.types.Selection`
* `vscode.window.TextEditor` has 1 child classes:
  * `vscode.window.ActiveTextEditor`

## API

### `vscode/`

The module is stable:
0 lines added or removed
in the last 4 weeks.

#### `vscode/compiler.py`

The file is stable:
0 lines added or removed
in the last 4 weeks.

Some important objects are:

**build**

```python
build(extension: Extension, publish: bool = False, config: dict = None) -> None
    Builds the extension.
    If variable config is None, config is an empty dict.
    If the extension publisher is None, the config publisher is user input.
    The function measures the time taken to run the function.
```

#### `vscode/config.py`

The file is stable:
0 lines added or removed
in the last 4 weeks.

#### `vscode/data.py`

The file is stable:
0 lines added or removed
in the last 4 weeks.

#### `vscode/env_methods.py`

The file is stable:
0 lines added or removed
in the last 4 weeks.

#### `vscode/extension.py`

The file is stable:
0 lines added or removed
in the last 4 weeks.

Some important objects are:

**Extension**

```
Extension
  __init__(
    self,
    name: str,
    display_name: str,
    version: str,
    description: Optional[str] = None,
    categories: Optional[list] = None,
    config: List[Config] = [],
    vscode_version: Optional[str] = None,
    icon: Optional[str] = None,
    publisher: Optional[str] = None,
    repository: Optional[dict] = None,
    ) -> None
        An error is raised if there is a space in name.

  register_command(
        self,
        func: Callable,
        name: Optional[str] = None,
        title: Optional[str] = None,
        category: Optional[str] = None,
        keybind: Optional[str] = None,
        when: Optional[str] = None,
    ) -> None
        The name variable is a function name if the name variable is None.

  event(self, func: Callable[[], str])
        A decorator for adding event handlers
        The name variable is the function name with "on" removed.
        The function is added to event.
```

#### `vscode/themes.py`

The file is stable:
0 lines added or removed
in the last 4 weeks.

Some important objects are:

**BaseColorSet**

```python
BaseColorSet
    __init__(self, background: str, foreground: str, colors: list)
```

**ColorSet**

```python
ColorSet
    __init__(self, base: BaseColorSet, syntax: dict = None, ui: dict = None, terminal: dict = None, type: str = "dark")
```

**ColorTheme**

```python
ColorTheme
    __init__( self, name: str, display_name: str, version: str, type: str = "dark", description: str = None, publisher: str = None, keywords: list = None, icon: str = None)
```

#### `vscode/types.py`

This file defines classes
used elsewhere in the codebase.

The file is stable:
0 lines added or removed
in the last 4 weeks.

Some important objects are:

**Range**

```python
Range
    __init__(self, start: Position, end: Position)
        A range represents an ordered pair of two positions. It is guaranteed that start.isBeforeOrEqual(end)
```
```
    intersection(self, other)
        Returns undefined if end is less than other's start or other's end is left than start.
        start variable is the largest value of start and other's start.
        end variable is the smallest value of end and other's end.
        Returns a range of start and end.

    union(self, other)
        start variable is the smallest value of start and other's start.
        end variable is the largest value of end and other's end.
        Returns a range of start and end.
```

**Selection**

```python
Selection(Range)
    __init__(self, active: Position, anchor: Position, start: Position, end: Position)
        Represents a text selection in an editor.
```

#### `vscode/undef.py`

The file is stable:
0 lines added or removed
in the last 4 weeks.

#### `vscode/utils.py`

This file defines functions
used elsewhere in the codebase.

The file is stable:
0 lines added or removed
in the last 4 weeks.

Some important objects are:

**send_ipc**

```python
send_ipc(code: str, args: list=None)
    Makes json of code and args.
    code is the code parameter.
    args is an empty list if args is None
```

#### `vscode/webviews.py`

The file is stable:
0 lines added or removed
in the last 4 weeks.

#### `vscode/window.py`

A mix of functions
and classes.
Several objects are imported
from this file
around the codebase.

Some important objects are:

**TextEditor**

```python
TextEditor
    __init__(self, data: dict = None)
```

**ActiveTextEditor**

```python
ActiveTextEditor(TextEditor)
    create_webview(webview: Webview, column: ViewColumn = ViewColumn.one, options: dict = None) -> Webview
        Checks if webview is a Webview type, otherwise raises an error.
        Checks if column is a ViewColumn type, otherwise raises an error.
```

<!---Documatic-section-fixed: bottom1-start--->
## Extensions built using vscode-ext

Here's a list of some extensions built using vscode-ext. If you'd like to include your extension here feel free to create a PR.

- [Youtube](https://github.com/CodeWithSwastik/youtube-ext)
- [Wikipedia](https://github.com/SkullCrusher0003/wikipedia-ext)
- [Internet Search](https://github.com/Dorukyum/internet-search)
- [Virtual Assistant](https://github.com/SohamGhugare/vscode-virtual-assistant)
- [YoExtension](https://github.com/yo56789/YoExtension)
<!---Documatic-section-fixed: bottom2-end--->
