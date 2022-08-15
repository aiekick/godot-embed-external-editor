# Godot Embed External Editor

A GDExtension which allows embedding an external code editor such as Visual Studio Code directly into your Godot editor!

**[Quick Start Guide](#quick-start)**

![Preview Image](docs/preview.png)

# Features

- Automatically attach and detach external code editors.
  - Checks if the code editor is relevant for the given project (e.g. the project folder is opened inside of it) whenever possible.
  - A toggle button in the scene tab bar to manually attach and detach the external code editor.
- Supported external editors:
  - Only Visual Studio Code for now.

# Quick Start

- Ensure that
  - you are using Godot 4.
  - you are on Windows.
  - in Godot's editor settings, "Single-window mode" is **disabled** (otherwise dialogs will not appear in front of the code editor).
  - in Godot's editor settings, external code editor is enabled and correctly set up (double-clicking a script file in Godot's file explorer should open your editor of choice).
  - you follow [the setup instructions](#per-editor-setup) for the editor of your choice.
- [Download the latest release](https://github.com/redmser/godot-embed-external-editor/releases) or build from source.
- Copy the `addons` folder into your project folder.
- Restart the Godot editor (gdextensions are not live reloaded).
- Enable the plug-in in the project settings.
- Open your code editor by double-clicking a file in Godot's explorer (unrelated code editors will NOT be embedded by this addon).
- Switch to the Script tab and enjoy!

## Per-Editor Setup

### Visual Studio Code

- In the settings, set `window.titleBarStyle` to `native`. Otherwise the titlebar can not be hidden and the editor window will be resizable independently from its container.
- Unless you modified it manually, the `window.title` setting contains both the string `Visual Studio Code` and the name of the currently open folder `${rootName}`. This is needed in order for the addon to detect whether the instance has the project opened.

# Limitations

This addon is very experimental and hacky. I'm trying to improve upon it, but there are some things that can not be fixed as easily:

## General

- Godot still has problems detecting external script file changes (see [this PR](https://github.com/godotengine/godot/issues/49298)).
  - **Workaround:** Restarting the editor with "Project -> Reload current project".
- Can not view documentation in editor without detaching editor.
  - **Workaround:** You can use VSCode's "List native classes" option as an alternative.
- There has been occasional freezes in the past which I've tried to fix. If they still persist, please [open an issue](https://github.com/redmser/godot-embed-external-editor/issues/new).
  - **Workaround:** If you get a freeze, it seems like Alt+Tab fixes it most of the time.
- Editor's titlebar does not show after undocked.
  - **Workaround:** Minimize and restore the window.
- Keyboard input will only be accepted by whichever window is in focus (e.g. F5 to run the game).
  - **Workaround:** You must click on the window that should receive focus first.
- Hover thumbnails for scene tabs do not show in front of the embedded code editor.

## Visual Studio Code

- Until [this PR](https://github.com/godotengine/godot-vscode-plugin/pull/400) is finished and merged, debugging code is not possible.
- Rarely, a black strip appears at the top of VSCode which offsets all input events
  - **Workaround:** Restart VSCode to fix this (sadly not even the "Reload Window" command solves this).