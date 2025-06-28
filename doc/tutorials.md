# Mezzano Tutorials

This document provides step-by-step tutorials for common tasks in Mezzano.

## Tutorial 1: Exploring the File System with Filer

The Filer application allows you to navigate and manage files and directories.

1.  **Open a REPL:** If you don't have one open, press `M-F10` (Alt + F10).
2.  **Launch Filer:** In the REPL, type `(mezzano.gui.filer:spawn)` and press Enter.
    *   A new window titled "Filer" should appear.
3.  **Navigating Directories:**
    *   The main part of the window lists files and directories in the current path (shown at the top).
    *   Double-click a directory to enter it.
    *   Use the "Up" button or icon (often `[..]`) to go to the parent directory.
4.  **Opening a File:**
    *   To open a file (e.g., a text file), try double-clicking it. This will usually open it in the default application, which is often the text editor for text files.
    *   For example, navigate to `/USER/` (or a similar directory if it exists) and see if there are any sample text files.
5.  **Closing Filer:** You can close the Filer window like any other application window, typically using `M-F4` or by clicking a close button if available.

## Tutorial 2: Basic Text Editing

Mezzano includes a text editor with Emacs-like keybindings.

1.  **Launch the Editor:**
    *   **Option A: From Filer:** Navigate to a directory in Filer (see Tutorial 1), then right-click (if supported) or find a menu option to create a new text file. Or, double-click an existing text file.
    *   **Option B: From REPL (opening a specific file):** If you know the path to a file, you might be able to open it directly. The command `(edit "filepath")` or similar might work. For example: `(edit "/USER/new-file.txt")`. (Note: The exact `edit` command may vary; check `user-manual.md`).
    *   **Option C: From REPL (for a new buffer):** You can often open the editor with an empty buffer. Try `(mezzano.gui.editor:spawn-editor)` or simply `(edit)` in the REPL.
2.  **Basic Text Input:**
    *   Once the editor window is open, you can type text directly.
    *   Navigate the cursor using arrow keys or Emacs keybindings (e.g., `C-F` for forward, `C-B` for backward, `C-N` for next line, `C-P` for previous line). See `user-manual.md` for a list of editor commands.
3.  **Saving a File:**
    *   Press `C-X C-S` (Ctrl+X then Ctrl+S).
    *   If the file is new or doesn't have a path, the editor will prompt you for a location and filename at the bottom (in the "minibuffer"). Type the full path (e.g., `/USER/my-document.txt`) and press Enter.
4.  **Saving with a New Name/Path (Save As):**
    *   Press `C-X C-W` (Ctrl+X then Ctrl+W).
    *   Enter the new path and filename when prompted.
5.  **Closing the Editor:**
    *   If you want to close just the current file buffer: `C-X k`. You might be asked to save if there are unsaved changes.
    *   To close the editor application window: `M-F4`.

## Tutorial 3: Using the REPL for Interaction

The REPL (Read-Eval-Print Loop) is a powerful tool for interacting with Mezzano.

1.  **Open a REPL:** Press `M-F10` (Alt + F10).
2.  **Evaluating Lisp Expressions:**
    *   Type any valid Common Lisp expression at the prompt and press Enter.
    *   Examples:
        *   `(+ 10 20)` (should return `30`)
        *   `(format t "Hello, Mezzano!~%")` (should print the string and return `NIL`)
        *   `(loop for i from 1 to 5 collect (* i i))` (should return `(1 4 9 16 25)`)
3.  **Inspecting System State:**
    *   The `(room)` function shows memory usage:
        *   `(room)` or `(room t)` for a detailed report.
    *   You can inspect variables or call functions related to the system. For example, to see information about the current thread (this is advanced): `(describe mezzano.supervisor::*current-thread*)`
4.  **Using History:**
    *   Press `M-P` (Alt+P) or Up-Arrow to recall previous commands.
    *   Press `M-N` (Alt+N) or Down-Arrow to move to newer commands in history.
5.  **Auto-completion:**
    *   Start typing a symbol name (e.g., `mezzano.gui.`) and press `Tab`. The system will try to complete the name or show possible completions.

## Tutorial 4: Taking a System Snapshot

Snapshots save the entire state of your Mezzano system.

1.  **When and Why to Take a Snapshot:**
    *   Before shutting down your VM to save your current work and window layout.
    *   After making significant configuration changes.
    *   Periodically, as a backup of your current session.
2.  **Ensure No Critical Operations are Running:** While snapshotting is generally safe, it's good practice to ensure no disk-intensive or highly stateful operations are in mid-process if avoidable.
3.  **Open a REPL:** If one isn't already open, press `M-F10`.
4.  **Execute the Snapshot Command:**
    *   In the REPL, type `(mezzano.supervisor:snapshot)` and press Enter.
5.  **Observe the Blinkenlights:**
    *   A yellow light will illuminate in the status area at the top-left of the screen. This indicates that the snapshot process is active.
    *   **Do not turn off the VM while the yellow light is on.**
6.  **Snapshot Complete:**
    *   Once the yellow light turns off, the snapshot is complete and saved to disk.
7.  **Continuing or Shutting Down:**
    *   You can continue using Mezzano.
    *   You can now safely power off your virtual machine. When you next start Mezzano, it will boot from this most recent snapshot, restoring your session.

These tutorials should help you get comfortable with some of the basic operations in Mezzano. Refer to the `user-manual.md` for more comprehensive details on all features.
