## Namespace Generator

This plugin will generate files that will organize your classes somewhat like a namespace. This doesn't change any functionality like I would expect an actual namespace implementation would, but it removes the need to create classes full of preloads manually and updating the files when you want to move reorganize.

<img width="395" height="58" alt="namespace_hl" src="https://github.com/user-attachments/assets/9556356b-c00f-4c51-bca0-ed8cd4252e37" />

## Install

This plugin uses external dependencies packaged with [GDPackage](https://github.com/brohd11/godot-gdpackage.git),
download the latest package from releases, it includes the required dependencies.

The dependency repos can be found in the require key of [plugin.cfg](./plugin.cfg)

You can also use [gdaddon](https://github.com/brohd11/gdaddon) to manage the installation.
It is a TUI package/repo manager that can install and update addons for you.

In your project:
```sh
gdaddon install brohd11/godot-namespace/release
```


## How to Use

Note: Before running the generator script, save all open scripts.

Choose where your script will live in the namespace, near the top of the file, define your desired class path:
``` 
extends SomeClass
#! namespace MyNameSpace.SubSpace class ThisClass
```

This layout generates 2 files, `MyNameSpace` a global class that preloads `SubSpace`. Intermediate classes need to be actual files, because inner classes will cause script caching errors when re-generating.

Once you have your files laid out, you can build a couple of ways:
- Run the editor script `res://addons/namespace/run_editor.gd`
- Run from [Editor Console](https://github.com/brohd11/godot-editor-console): `namespace build`
- Run from command line: `godot --headless --path . --script res://addons/namespace/run_headless.gd [-- <flags>]`

If there are existing namespace files it will parse all scripts in your project to check if your new configuration will break any references. It will list any conflicts and you can decide to proceed or not, before the existing files are deleted and regenerated.

### Generation Directory

By default, the namespace files are generated in `res://namespace_classes/`. You can change this in project settings or using Editor Console `namespace set-dir <my/dir>`.

You can also change where certain namespaces are created by setting up a namespace config file. Accepted files are `plugin.cfg`, `package.cfg`, and `namespace.cfg`. There should be a section `[namespace]` with a path key, `path=""`. An empty path defaults to `_ns/`, otherwise declare a relative path.

```ini
[namespace]
path="ns"
```

Any files found with the config file's tree will be generated within the `path` directory. This is useful for something like a plugin or a library where you want to keep the generate files within the package.


## Other Plugins

These plugins used to be packaged with this one. They are now separately managed to reduce the size of this release. They can be downloaded and will provide some nice features.

### SyntaxPlus

If you have the [SyntaxPlus](https://github.com/brohd11/godot-syntax-plus.git) syntax highlighter active, there will be a few (configurable) colors that you will see when defining the namespace. These can be adjusted in Editor Settings.

These will always apply:
 - Green - A new namespace or class declaration
 - Red - Name clash with global script or built-in type

These will appear once files are generated:
 - Dark Blue - Existing namespace or class
 - Light Blue - The current script's namespace location
 - Dark Red - Name clash with another member in the namespace

### Code Completions

With the [Code Completions](https://github.com/brohd11/godot-code-completions) plugin, you will get completions for the
namespace tag and existing name spaces and sub spaces.

### Editor Console

There are a few commands you can run from the console. 

