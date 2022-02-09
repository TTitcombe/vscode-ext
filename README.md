<!---Documatic-section-fixed: top1-start--->
<p align="center">
  <img alt="vscode logo" src="https://github.com/CodeWithSwastik/vscode-ext/blob/main/images/vscode-ext-2.png?raw=true" width='500px'/>
</p>

<p align="center"><a href="https://GitHub.com/CodeWithSwastik/vscode-ext/graphs/commit-activity"><img src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" alt="Maintenance"></a>
<a href="https://pepy.tech/project/vscode-ext"><img src="https://static.pepy.tech/personalized-badge/vscode-ext?period=total&amp;units=international_system&amp;left_color=orange&amp;right_color=brightgreen&amp;left_text=Downloads" alt="Downloads"></a>
<a href="https://pypi.python.org/pypi/vscode-ext/"><img src="https://badge.fury.io/py/vscode-ext.svg" alt="PyPI version"></a>
<a href="https://github.com/psf/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>

**Last updated:** 2022-02-09\
_Document generation aided by [**Documatic**](www.documatic.com)_

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

<!---Documatic-section-group: helloworld-start--->


## Getting Started

<!---Documatic-section-helloworld: setup-start--->
* The codebase has a flat structure, with 12 code files.
* The codebase is compatible with Python 3.6 and above (f-strings in e.g. `vscode-ext/vscode/themes.py`)
* Install requirements with `pip install -r requirements.txt` or install directly from pypi:

```
pip install vscode-ext
```

<!---Documatic-section-helloworld: setup-end--->

<!---Documatic-section-helloworld: entrypoints-start--->


### Code Overview

There are 23 source code objects in top-level `__main__`/`__init__`.
Some key functions include:

### `build` from `vscode/compiler.py`
 
```python
build(extension: Extension, publish: bool=False, config: dict=None) -> None

The code has a high cyclomatic complexity.
Builds the extension.
extension - Attributes of the object are read to build a config
config - A configuration dictionary of variables
Calls several internal functions,
such as `build_py`, `build_js`.
```

### `build_theme` from `vscode/compiler.py`
 
```python
build_theme(theme: ColorTheme, config: dict=None)

This function takes a theme object and a config object.
If the config is None, it creates an empty config object.
Checks theme for attributes to populate the config object.
The code has a high cyclomatic complexity.
Builds the files needed for the theme.
Calls several internal functions,
such as `create_theme_package`, `create_theme_files`.
```

These entrypoints are broken down into the following modules:

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

#### vscode.extension.Extension

Some key methods include:

```python
Extension
        Represents a vscode extension

command(name, title, category, keybind, when)
        A decorator.
        Runs internal method `register_command`.

register_command(func, name, title, category, keybind, when)
        Uses the default_category attribute of the class if category is None.
        Creates a Command.
        If a keybind is given, registers a keybind for the Command.
        Adds the Command to a list of commands.
```

#### Inheritance

The project's class inheritance structure is:

* `vscode.types.Range` has 1 child classes:
  * `vscode.types.Selection`
* `vscode.window.TextEditor` has 1 child classes:
  * `vscode.window.ActiveTextEditor`


<!---Documatic-section-helloworld: entrypoints-end--->

<!---Documatic-section-group: concept-start--->
## Examples

### Quickstart

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

<!---Documatic-section-group: concept-end--->

<!---Documatic-section-group: helloworld-end--->

<!---Documatic-section-group: dev-start--->


## Developers
<!---Documatic-section-dev: ci-start--->
* Install locally with `pip install -e .`
* vscode-ext does not contain unit tests
* The project uses GitHub Actions for CI/CD

| CI File | Purpose |
|:----|:----|
| docs | Executes on push for branch main. Builds docs |


<!---Documatic-section-dev: ci-end--->

<!---Documatic-section-group: dev-end--->

### **vscode-ext/**

#### themes.py

```python
global_setting_generator(name: str)

This function takes a name of a setting, and returns a function that takes a color and returns a dictionary with the setting name as the key and the color as the value.
This function is a generator, so you can use it in a for loop to iterate over all the colors.
```

```python
simple_color_generator(name: str, scope: str, font_style: int = FontStyle.NONE)

The function is a generator.
It returns a generator object.
The generator object has a __next__() method.
```

```python
lighten(color: str, amount: int) -> str

This function takes a color and an amount.
It returns a lighter color.
The color is a tuple of three integers between 0 and 255.
```

```python
add_alpha(color: str, alpha: int) -> str

This function takes a color and an alpha value and returns a new color.
The color must be in #rrggbb format.
The code has a high cyclomatic complexity.
Raises ValueError.
```

```python
generate_fallback_color_set(s: BaseColorSet, type: str) -> ColorSet

This function takes a string and a type, and returns a color set.
The type can be 'light' or 'dark'.
```

```python
generate_theme(name: str, color_set: ColorSet) -> dict
```

```python
contrast(color: str) -> str

The function takes a color as a parameter.
It checks if the color is None.
If it is, it returns None.
This is a Python idiom.
It means that if the color is None, then the function returns None.
```

#### compiler.py

```python
create_package(data: dict, config: dict) -> dict
```

```python
build(extension: Extension, publish: bool=False, config: dict=None) -> None

The code has a high cyclomatic complexity.
Builds the extension.
Parameters:
- extension: The extension to build
- publish: If `True`, files needed for publishing will be created
```

```python
build_theme(theme: ColorTheme, config: dict=None)

This function takes a theme object and a config object.
It checks if the config object is None.
If it is, it creates a new config object.
The code has a high cyclomatic complexity.
Builds the files needed for the theme.
```

#### types.py

This file defines classes
used elsewhere in the codebase.

The file is stable:
0 lines added or removed
in the last 4 weeks.

#### utils.py

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

#### window.py

A mix of functions
and classes.
Several objects are imported
from this file
around the codebase.

<!---Documatic-section-fixed: bottom1-start--->
## Extensions built using vscode-ext

Here's a list of some extensions built using vscode-ext. If you'd like to include your extension here feel free to create a PR.

- [Youtube](https://github.com/CodeWithSwastik/youtube-ext)
- [Wikipedia](https://github.com/SkullCrusher0003/wikipedia-ext)
- [Internet Search](https://github.com/Dorukyum/internet-search)
- [Virtual Assistant](https://github.com/SohamGhugare/vscode-virtual-assistant)
- [YoExtension](https://github.com/yo56789/YoExtension)
<!---Documatic-section-fixed: bottom2-end--->

_Document generation aided by [**Documatic**](www.documatic.com)_
