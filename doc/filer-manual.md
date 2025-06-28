# Mezzano Filer Manual

The Filer is Mezzano's graphical file manager. It allows you to navigate directories, view available storage hosts, and open files.

## Launching Filer

You can launch the Filer from the REPL using the following command:

```lisp
(mezzano.gui.filer:spawn &key initial-path width height)
```

*   `&key initial-path`: Specifies the starting directory. Defaults to the system's current default path (`*default-pathname-defaults*`).
    *   Example: `(mezzano.gui.filer:spawn :initial-path "LOCAL:>Users>Someone>")`
*   `&key width height`: Specifies the initial width and height of the Filer window in pixels.
    *   Example: `(mezzano.gui.filer:spawn :width 800 :height 600)`

## The Filer Window

The Filer window consists of several parts:

*   **Title Bar:** Displays the full path of the currently viewed directory. It also contains standard window controls like a close button. The window is resizable.
*   **Host List:** At the top of the content area, a list of available storage hosts (e.g., `LOCAL:`, `REMOTE:`) is displayed. Clicking a host name will navigate to the root of that host.
*   **Current Path Display:** Below the host list, the current path is displayed again.
*   **Content Area:** This is the main part of the window, listing directories and files within the current path.
    *   Directories are usually listed first, followed by files. Both are sorted alphabetically.
    *   Each entry is typically preceded by an icon:
        *   ![Up Icon](placeholder_up_icon.png) **Parent Directory (`..`):** An icon representing "up" or "parent" will be shown if you are not in the root directory of a host. Clicking this navigates one level up.
        *   ![Folder Icon](placeholder_folder_icon.png) **Directory:** Indicates a directory.
        *   ![File Icon](placeholder_file_icon.png) **File:** Indicates a file.
    *   File names are color-coded based on their type to help distinguish them (e.g., Lisp source files, text files, media files). These colors are defined by the system theme.

## Navigation

*   **Changing Directories:** Double-click (or single-click, depending on system settings) on a directory name or its icon to enter that directory.
*   **Going to Parent Directory:** Click the "Parent" entry (often represented by `..` or an "up" arrow icon) to navigate to the directory containing the current one.
*   **Switching Hosts:** Click on a host name in the host list at the top (e.g., `LOCAL:`) to switch to the root directory of that host.

## Opening Files

To open a file, click on its name or icon. Mezzano will attempt to launch the default application associated with that file type:

*   **Text Files:** (e.g., `.lisp`, `.txt`, `.md`, `.asd`) will typically open in the Mezzano Text Editor.
*   **Image Files:** (e.g., `.png`, `.jpg`) will open in the Image Viewer (`mezzano.gui.image-viewer`).
*   **Video Files:** (e.g., `.avi`, `.gif` - if treated as video) will open in the Media Player (`mezzano.gui.trentino`).
*   **Audio Files:** (e.g., `.wav`) will open in the Music Player (`mezzano.gui.music-player`).

The Filer determines the file type based on its extension.

## Current Limitations

The Mezzano Filer is primarily a navigator and file opener. As of this writing, it does **not** support features like:

*   Creating new files or directories.
*   Deleting, renaming, copying, or moving files/directories.
*   Viewing detailed file properties (like size or modification date).
*   Context menus (right-click functionality).
*   Direct path input via an address bar.
*   Bookmarks or favorite locations.

For file modification tasks, you would typically use commands in the REPL or functionality within specific applications (like saving a file from the Editor).

*(Note: Placeholder image links like `placeholder_up_icon.png` should be replaced with actual paths to icons if available and displayable in the documentation system, or removed if markdown doesn't support images well here.)*
