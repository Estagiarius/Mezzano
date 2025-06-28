Welcome to the Mezzano User Manual. This document provides detailed information about Mezzano's features, built-in applications, and system usage.

For a guide on setting up Mezzano for the first time, please see the [Getting Started Guide](getting-started.md).
For answers to common questions, refer to the [FAQ](faq.md).
For step-by-step examples of common tasks, see the [Tutorials](tutorials.md).

# Basic functionality

`C-<key>` means to hold the control key while typing `<key>`.

`M-<key>` means to hold the alt or meta key while typing `<key>`.

Alphabetic keys typed with control or meta ignore case. `C-A` and `C-a` are the same key, while `C-!` and `C-1` are different.

The default keymap is En-GB, use M-F12 to switch between En-GB, En-US, No-BK, PanCyr, German, and ES-ESP keymaps.
Windows can be moved by dragging their titlebar or by holding the Alt key and dragging.

# Global Shortcut Keys

`M-F12`        Switch to the next keymap.

`C-M-F12`      Switch to the previous keymap.

`M-F11`        Print debugging information to the serial port.

`M-F10`        Open a REPL.

`C-M-F10`      Open a less featureful REPL.

`M-Esc`        Attempt to interrupt the thread associated with the current window.

`C-M-Esc`      Like `M-Esc`, but use `CERROR` instead of `BREAK`.

`M-F1`         Force the compositor to redraw the whole screen.

`M-F4`         Quit the current application.

`C-M-F4`       Forcibly close the current window.

# Line editing

The line editor supports most standard line navigation and editing commands.

`C-F`          Move forward (right) one character, also bound to Right-Arrow.

`C-B`          Move backward (left) one character, also bound to Left-Arrow.

`C-A`          Move to beginning of line, also bound to Home.

`C-E`          Move to end of line, also bound to End.

`M-F`          Move forward one word.

`M-B`          Move backward one word.

`M-P`          Find previous (older) matching history item, also bound to Up-Arrow.

`M-N`          Find next (newer) matching history item, also bound to Down-Arrow.

`C-D`          Delete the next character, also bound to Delete.

`Backspace`    Delete the previous character.

`M-D`          Delete the next word.

`M-Backspace`  Delete the previous word.

`C-K`          Delete from the cursor to the end of the line.

`C-C`          Enter the debugger using BREAK.

`C-G`          Invoke the most recent ABORT restart. This will usually clear any input and return you to a prompt.

`Tab`          Cycle through completions for the current symbol.

# Editor

Mezzano includes a powerful text editor with Emacs-like keybindings, suitable for general text editing and Lisp development. For a detailed explanation of its features, concepts (buffers, files, regions, kill/yank, Lisp interaction), and a full guide, please see the [Mezzano Text Editor Manual](editor-manual.md).

Launch the editor using the `(edit)` command or `(mezzano.gui.editor:spawn-editor)`:
*   `(edit)` or `(mezzano.gui.editor:spawn-editor)`: Opens a new, empty buffer.
*   `(edit "path/to/file")`: Opens the specified file.

## Common Editor Keybindings

Here is a summary of common keybindings. Refer to the [Editor Manual](editor-manual.md) for more context.

**Movement:**
`C-F` / `Right-Arrow`: Forward character
`C-B` / `Left-Arrow`: Backward character
`C-N` / `Down-Arrow`: Next line
`C-P` / `Up-Arrow`: Previous line
`C-A` / `Home`: Beginning of line
`C-E` / `End`: End of line
`M-F` / `M-Right-Arrow`: Forward word
`M-B` / `M-Left-Arrow`: Backward word
`M-<` / `Home` (sometimes): Beginning of buffer
`M->` / `End` (sometimes): End of buffer
`C-V` / `Page-Down`: Page down
`M-V` / `Page-Up`: Page up
`C-M-F`: Forward s-expression
`C-M-B`: Backward s-expression
`C-C C-A`: Move to start of current top-level Lisp form

**Editing (Deleting/Killing):**
`C-D` / `Delete`: Delete next character
`Backspace`: Delete previous character
`M-D`: Kill next word
`M-Backspace`: Kill previous word
`C-K`: Kill from cursor to end of line (or newline if at EOL)
`C-M-K`: Kill next s-expression
`C-W`: Kill region (between point and mark)

**Yanking (Pasting):**
`C-Y`: Yank last killed text

**Mark and Region:**
`C-Space`: Set mark / Deactivate mark
`C-X C-X`: Swap point and mark

**File Operations:**
`C-X C-F`: Open or create a file
`C-X C-S`: Save current buffer
`C-X C-W`: Save buffer with new path

**Buffer Management:**
`C-X b`: Switch to a different buffer
`C-X C-B`: List buffers
`C-X k`: Close (kill) current buffer

**Lisp Interaction:**
`C-C C-C`: Evaluate current top-level Lisp form
`M-x repl`: Create an editor-based REPL

**Miscellaneous:**
`C-L`: Recenter display
`M-L`: Redraw screen
`C-Q`: Insert next key typed literally
`C-G`: Abort current command

# Applications

Mezzano comes with several built-in applications. These are typically launched by typing a Lisp command in the REPL. Common applications include:

*   **Filer:** A graphical file manager. See the [Filer Manual](filer-manual.md) for detailed information.
    *   Launch (example): `(mezzano.gui.filer:spawn)`
*   **Peek:** A system information tool. View running tasks, memory, network configuration, etc. See the [Peek Manual](peek-manual.md) for detailed information.
    *   Launch (example): `(mezzano.gui.peek:spawn)`
*   **Editor:** A text editor with Emacs-like keybindings. See the [Editor Manual](editor-manual.md) for full details.
    *   Launch (example, new buffer): `(edit)` or `(mezzano.gui.editor:spawn-editor)`
    *   Launch (example, specific file): `(edit "/path/to/your/file.txt")`
*   **Memory Monitor:** Displays graphs and bitmaps of virtual and physical memory usage.
    *   Launch (example): `(mezzano.gui.memory-monitor:spawn)`
*   **IRC Client:** For connecting to IRC servers. See the [IRC Client Manual](irc-manual.md) for detailed information.
    *   Launch (example): `(mezzano.application.irc:spawn)`
*   **Telnet Client:** For connecting to Telnet servers. See the [Telnet Client Manual](telnet-manual.md) for detailed information.
    *   Launch (example): `(mezzano.application.telnet:spawn)`
*   **Mandelbrot:** `(mezzano.mandelbrot:spawn &optional width height)`
    This application renders a colourful visualization of the Mandelbrot set or a Julia set. The window displays the fractal, which is drawn progressively.
    *   Press `M` to view the Mandelbrot set (default).
    *   Press `J` to switch to viewing a predefined Julia set.
    The fractal's colours will vary subtly with each full redraw as they are influenced by the current time. The window is resizable, and resizing will trigger a recalculation and redraw of the fractal.
*   **Spy:** `(mezzano.gui.spy:spawn)`
    A developer utility for inspecting the internal state of the GUI compositor and input systems. The Spy window displays a text-based stream of information that updates periodically. This includes current mouse coordinates and button states, the window under the mouse, active drag operations, the current system keymap, keyboard modifier states, a list of all windows, and other low-level GUI details. This tool is primarily useful for debugging GUI behavior.
*   **Settings:** `(mezzano.gui.settings:spawn)`
    This application allows you to configure basic system settings. Currently, its primary function is to **change the system keyboard layout (keymap)**. Upon launching, it displays a list of available keymaps (e.g., En-GB, En-US, German). Clicking on one of these buttons immediately switches the system's active keymap to the selected layout. The currently active keymap button is typically highlighted.

*Note: The exact launch commands might vary. Some applications might also be launchable from a system menu if one is available in your Mezzano version.*

# Networking

Mezzano supports networking with specific hardware and configurations:

*   **Supported NICs:** RTL8168 and virtio-net are the primary supported network interface cards.
    *   When using VirtualBox, the **Intel PRO/1000 MT Desktop (82540EM)** adapter (often a default for Linux VMs) is generally compatible as it can operate in a mode that Mezzano supports.
    *   For QEMU, `virtio-net` is recommended.
*   **Configuration:** Network settings can be viewed using the "Network" pane within the **Peek** application.
*   **Default Network:** The default network setup is often tailored for NAT configurations in VirtualBox and QEMU.
*   **Limitations:**
    *   **DHCP is not currently supported.** IP addresses and network settings typically need to be configured manually or rely on the VM's NAT providing a usable static configuration.
    *   Bridging to a real network (to get an IP on your LAN) is not supported out-of-the-box and would require manual setup.

# Whole-system transparent persistence support

Run `(mezzano.supervisor:snapshot)` in a REPL.
Wait for the yellow light to turn off.
Reboot.

This will take a snapshot of the current machine state, saving it to disk.
It will be restored when the machine is booted.

# Blinkenlights

A number of status lights are displayed at the top left of the screen.
From left to right:

`Green`        Disk read in progress.

`Red`          Disk write in progress.

`Purple`       GC in progress.

`Cyan`         Activity, system is not idle.

`Yellow`       Snapshot in progress.

`Brown`        Page fault being serviced.

`Light Green`  Network activity.

* The entire top line will turn red if the system panics.

# Memory Monitor

The Memory Monitor application provides a visual display of physical and virtual memory usage. It helps in understanding how memory is allocated and utilized by the system.

**Launch Command:** `(mezzano.gui.memory-monitor:spawn &optional width height)`

The Memory Monitor has two main modes, which can be switched using keyboard shortcuts or by clicking tabs at the top of the window:
*   **Graphs Mode (Press 'G' or click "Graphs" tab):** This is often the default mode. It displays scrolling line graphs for various virtual memory metrics over time.
*   **Physical Visualizer Mode (Press 'P' or click "Physical Visualizer" tab):** This mode displays a bitmap where each pixel or small block represents a page (or group of pages) of physical memory, colored according to its current usage type.

Press `Space` to refresh the current view.

## Graphs Mode Details

In Graphs Mode, several metrics are tracked:

*   **General Area Usage (%):** Percentage of the general-purpose memory area currently in use.
*   **General Area Bytes Allocated:** Total bytes allocated in the general area (autoscaled graph).
*   **General Area Bytes Committed:** Total bytes committed in the general area (autoscaled graph).
*   **Cons Area Usage (%):** Percentage of the memory area dedicated to Lisp cons cells currently in use.
*   **Cons Area Bytes Allocated:** Total bytes allocated in the cons area (autoscaled graph).
*   **Cons Area Bytes Committed:** Total bytes committed in the cons area (autoscaled graph).
*   **Pinned Area Usage (%):** Percentage of memory pinned for specific purposes (e.g., DMA).
*   **Wired Area Usage (%):** Percentage of memory wired down (cannot be paged out).
*   **Function Area Usage (%):** Percentage of memory used for compiled function code.
*   **Wired Function Area Usage (%):** Percentage of function area memory that is wired.

**Graph Colours:**
The colours for the lines in the Graphs Mode correspond to specific metrics:

*   **General Area % Usage:** `Dark Blue` (controlled by `theme:*memory-monitor-general-area-usage*`)
*   **General Area Bytes Allocated:** `Purple` (controlled by `theme:*memory-monitor-general-area-alloc*`)
*   **General Area Bytes Committed:** (controlled by `theme:*memory-monitor-general-area-commit*`)
*   **Cons Area % Usage:** `Green` (controlled by `theme:*memory-monitor-cons-area-usage*`)
*   **Cons Area Bytes Allocated:** `Lime Green` (controlled by `theme:*memory-monitor-cons-area-alloc*`)
*   **Cons Area Bytes Committed:** (controlled by `theme:*memory-monitor-cons-area-commit*`)
*   **Pinned Area % Usage:** `Red` (controlled by `theme:*memory-monitor-pinned-area-usage*`)
*   **Wired Area % Usage:** `Hot Pink` (controlled by `theme:*memory-monitor-wired-area-usage*`)
*   **Function Area % Usage:** `Brown` (controlled by `theme:*memory-monitor-function-area-usage*`)
*   **Wired Function Area % Usage:** `Lilac` (controlled by `theme:*memory-monitor-wired-function-area-usage*`)

The graph background is typically a dark color (controlled by `theme:*memory-monitor-graph-background*`), and a vertical tracker line indicates the current sampling point (controlled by `theme:*memory-monitor-graph-tracker*`).

## Physical Visualizer Mode Details

This mode displays a bitmap indicating how each page of physical memory is used.

**Physical Memory Colours:**
These colours indicate the status of physical memory pages:

`Blue`         Free memory.

`Red`          Wired memory.

`Brown`        Wired backing memory, used during a snapshot.

`Green`        Active in-use memory.

`Dark green`   Active in-use memory ready to be written to disk.

`Purple`       Inactive memory ready to be written to disk.

`Pink`         Page tables.

`Grey`         Other.

`White`        Mixture.

`Black`        Unused or not present.

# Swank

This release includes Swank 2.24.
The Swank server is listening on port 4005.

Forwarding for port 4005 will need to be enabled in the virtual
machine's settings. In VirtualBox this is done throught the port
forwarding settings, which can be accessed through
Settings -> Network -> Advanced -> Port Forwarding
