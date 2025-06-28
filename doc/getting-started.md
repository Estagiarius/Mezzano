# Getting Started with Mezzano

Welcome to Mezzano! This guide will help you take your first steps with this Common Lisp-based operating system.

## 1. Obtaining Mezzano

The easiest way to try Mezzano is by using pre-built demo releases.
*   **Download:** You can find these on the [Mezzano GitHub Releases page](https://github.com/froggey/Mezzano/releases).
*   Download the latest `.zip` file (e.g., `Mezzano-Demo4-r2600.zip`).
*   Extract the archive. You'll find a disk image file (e.g., `Mezzano.vmdk` for VirtualBox or `Mezzano.qcow2` for QEMU).

## 2. Recommended Virtual Machine Setup

Mezzano is primarily designed to be run in a virtual machine. Here are some recommended settings:

*   **Virtualization Software:** VirtualBox (recommended) or QEMU.
*   **RAM:** At least 2GB.
*   **NIC (Network Interface Card):**
    *   For **VirtualBox**, an **Intel PRO/1000 MT Desktop (82540EM)** adapter is a common choice (often the default for Linux VMs).
    *   For **QEMU**, a `virtio-net` device is generally recommended.
    *   Mezzano also supports other NICs like RTL8168. For more details on network configuration and supported hardware, please see the `user-manual.md` and `faq.md`.
*   **Audio Controller:** Intel HDA (High Definition Audio).
*   **Disk Image:** Use the downloaded Mezzano disk image as the primary hard disk for your VM.

Consult your virtualization software's documentation for instructions on creating a new VM and configuring these settings.

## 3. Your First Boot

Once your VM is configured:

1.  Start the virtual machine.
2.  Mezzano will boot, and you should see a desktop environment with status lights (blinkenlights) at the top-left.

## 4. Basic Interaction

Here's how to perform some initial actions:

*   **The REPL (Read-Eval-Print Loop):** The REPL is your primary interface for interacting with Mezzano at a low level.
    *   Press `M-F10` (Alt + F10) to open a new REPL window.
    *   You'll see a prompt like `CL-USER> `.
    *   Try a simple Lisp command: type `(+ 2 2)` and press Enter. Mezzano should respond with `4`.
*   **Windows:**
    *   You can move windows by clicking and dragging their title bars.
    *   Alternatively, hold the `Alt` key and click anywhere on a window to drag it.
    *   To close a window, you can often use `M-F4` (Alt + F4) for the current application, or `C-M-F4` (Ctrl + Alt + F4) to forcibly close it.
*   **Launching Applications:** Many applications can be launched from the REPL by typing their name (often prefixed with `mezzano.application.` or similar, or a specific launch command). For example, to try and launch the file manager:
    *   In the REPL, type `(mezzano.gui.filer:spawn)` and press Enter. (Note: The exact command might vary; consult the `user-manual.md` or experiment).
    *   Similarly, Peek (system information) can often be launched via `(mezzano.gui.peek:spawn)`.

## 5. Saving Your Work: Snapshotting

Mezzano uses a unique system called "snapshotting" to save the entire state of the operating system, including all open applications and data.

1.  **Open a REPL** (if you don't have one open).
2.  **Type the command:** `(mezzano.supervisor:snapshot)` and press Enter.
3.  **Wait:** A yellow light will appear in the "blinkenlights" area at the top-left of the screen. Wait for this light to turn off. This indicates the snapshot is complete.
4.  **Reboot:** You can now safely reboot or power off your VM. When you start Mezzano again, it will resume from the saved snapshot.

This is the primary way to "save your work" in Mezzano.

## 6. Where to Go Next

You've taken your first steps! To learn more about Mezzano:

*   **User Manual (`user-manual.md`):** For detailed information on keybindings, system features, and available applications.
*   **FAQ (`faq.md`):** For answers to common questions.
*   **Tutorials (`tutorials.md`):** For step-by-step guides on common tasks.

We hope you enjoy exploring Mezzano!
