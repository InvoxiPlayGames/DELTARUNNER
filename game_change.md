# DELTARUNNER Linux game_change implementation

DELTARUNNER's implementation of game_change differs a lot from Windows, and acts closely to how it behaves on macOS.

When game_change is invoked, DELTARUNNER:
* Sets environment variables to keep window state persistent. (inspired by macOS)
    * `GAMEMAKER_INITIAL_WINDOW_FS`, set to 1 if the game is in fullscreen.
    * `GAMEMAKER_INITIAL_WINDOW_FS_BORDERLESS` (unused)
    * `GAMEMAKER_INITIAL_WINDOW_X`, the X position of the window on the desktop.
    * `GAMEMAKER_INITIAL_WINDOW_Y`, the Y position of the window on the desktop.
    * `GAMEMAKER_INITIAL_WINDOW_WIDTH`, the width of the game window.
    * `GAMEMAKER_INITIAL_WINDOW_HEIGHT`, the height of the window.
* Adds a launch argument to scope the newly launched game.
    * `-gamedir chapter4_windows`
* Executes the runner with the new arguments and environment via `system()`, then exits the original process.

When the new process is loaded, the environment variables for storing window state are checked and then the correct values are set after initialising X, but before initialising the engine's graphics APIs. They're cleared once read.

The `-gamedir` launch argument changes the scope for file reads in the runner, prepending all bundle file reads with e.g. `./chapter4_windows/`. This differs from Windows and macOS where the current working directory is changed.

This process differs from macOS as there is no process fork and there is no pipe between the old and new process to indicate success and tell the launching process to quit.
