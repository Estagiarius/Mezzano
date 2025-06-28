# Mezzano Text Editor Manual

The Mezzano Text Editor provides a comprehensive environment for editing text files, particularly Lisp source code. It uses keybindings familiar to Emacs users. This manual explains the core concepts and functionalities beyond the basic keybindings listed in the main User Manual.

You can typically start the editor by:
*   Using the `(edit)` command in the REPL, optionally with a file path:
    *   `(edit)`: Opens a new, empty buffer.
    *   `(edit "LOCAL:>path>to>your>file.txt")`: Opens the specified file.
*   The Filer application will also use this editor to open text-based files.
*   The system may also refer to it as `(mezzano.gui.editor:spawn-editor)`.

## Core Concepts

### 1. Buffers

The editor works with **buffers**. A buffer is an in-memory workspace where you edit text.
*   When you open a file, its contents are loaded into a new buffer.
*   You can create empty buffers (e.g., with `(edit)` without arguments).
*   Changes you make are to the buffer in memory; they are not saved to the file on disk until you explicitly save.
*   **Multiple Buffers:** You can have multiple buffers open simultaneously.
    *   `C-X b` (Switch to Buffer): Prompts you to enter the name of another buffer to switch to.
    *   `C-X C-B` (List Buffers): Displays a list of all open buffers, often in a new temporary buffer. This list usually shows buffer names, associated file paths, and modification status.
    *   `C-X k` (Kill Buffer): Closes the current buffer. If the buffer has unsaved changes, you will typically be prompted to save them first.

### 2. Files

*   **Opening Files (`C-X C-F`):** This command prompts you for a file path.
    *   If the file exists, it's read into a new buffer.
    *   If the file does not exist, an empty buffer is created, associated with the new file name. The file itself is not created on disk until you save the buffer.
*   **Saving Buffers (`C-X C-S`):** Saves the contents of the current buffer to its associated file.
    *   If the buffer is not associated with a file (e.g., a new buffer), you will be prompted to enter a file path.
*   **Save As (`C-X C-W`):** Saves the contents of the current buffer to a new file path that you specify. This changes the buffer's association to the new file path.

### 3. The Point, Mark, and Region

*   **Point:** This is the current position of the cursor in the buffer. Most editing commands operate relative to the point.
*   **Mark (`C-Space`):** This command sets the "mark" at the current point. The mark is an invisible anchor.
    *   If the mark is already active and the point is at the mark, `C-Space` deactivates the mark.
*   **Region:** The text between the point and the mark is called the "region". Many commands operate on the current region.
*   **Swap Point and Mark (`C-X C-X`):** Exchanges the current position of the point with the position of the mark. This is useful for adjusting the boundaries of the region.

### 4. Killing and Yanking (Cut/Copy/Paste)

The editor uses a "kill and yank" system similar to Emacs.
*   **Killing Text:** Commands that delete more than one character (e.g., `C-K` for kill line, `M-D` for kill word forward, `C-W` for kill region) are "kill" commands. The killed text is stored in a conceptual "kill ring" (though the Mezzano User Manual refers to it as "last killed text," implying a simpler single-item storage).
    *   `C-K` (Kill Line): Deletes text from the point to the end of the line. If the point is at the end of the line, it kills the newline character.
    *   `M-D` (Kill Word Forward): Kills the word after the point.
    *   `M-Backspace` (Kill Word Backward): Kills the word before the point.
    *   `C-M-K` (Kill S-expression Forward): Kills the Lisp s-expression after the point.
    *   `C-W` (Kill Region): Kills the text within the currently defined region (between point and mark).
*   **Yanking Text (`C-Y`):** Inserts the most recently killed text at the current point. This is equivalent to "pasting."

### 5. Lisp Interaction

The editor has special support for Lisp code:
*   **S-expression Movement:**
    *   `C-M-F` (Forward S-expression): Moves the point forward over one s-expression.
    *   `C-M-B` (Backward S-expression): Moves the point backward over one s-expression.
*   **Evaluation:**
    *   `C-C C-C` (Evaluate Current Top-Level Form): Evaluates the Lisp top-level form (e.g., a `defun`, `defvar`) that the point is currently in or immediately after. Results are typically shown in a REPL or minibuffer.
*   **Navigating Forms:**
    *   `C-C C-A` (Move to Start of Current Top-Level Form): Moves the point to the beginning of the current top-level Lisp form.

### 6. Editor-Based REPL (`M-x repl`)

The command `M-x repl` (Meta-X followed by typing "repl" and Enter, if it uses minibuffer prompting similar to Emacs for M-x commands) creates a REPL (Read-Eval-Print Loop) environment within or associated with the editor. This allows for interactive Lisp development without leaving the editor.

## Other Notable Features (from Keybindings)

*   **Basic Movement:** Arrow keys, `C-A` (beginning of line), `C-E` (end of line), `M-<` (beginning of buffer), `M->` (end of buffer), `C-V` (page down), `M-V` (page up).
*   **Recenter Display:** `C-L` recenters the display around the point.
*   **Redraw Screen:** `M-L` redraws the screen.
*   **Abort Command:** `C-G` cancels the current multi-key command or operation.
*   **Insert Literal:** `C-Q` inserts the next typed key literally, without interpreting it as a command.

This manual provides an overview of the editor's conceptual model. For a full list of default keybindings, please refer to the "Editor commands" section in the main `user-manual.md`.
