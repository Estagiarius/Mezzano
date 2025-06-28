# Mezzano - Frequently Asked Questions (FAQ)

This FAQ provides answers to common questions about Mezzano.

**Q: How do I build Mezzano from source?**

A: Mezzano uses a custom build system called MBuild. You can find instructions and the MBuild repository here: [https://github.com/froggey/MBuild](https://github.com/froggey/MBuild). Building from source is recommended for developers or those wishing to contribute. For general use, pre-built images are available (see `getting-started.md`).

**Q: What hardware is supported?**

A: Mezzano is primarily designed for virtualization:
*   **VirtualBox:** This is the most common way to run Mezzano.
*   **QEMU:** Also well-supported.

Recommended virtual hardware:
*   **RAM:** 2GB or more.
*   **NIC:** Virtio-net is generally recommended. RTL8168 is also supported. The default Intel PRO/1000 series in VirtualBox usually works.
*   **Audio:** Intel HDA.

**Real Hardware:**
*   x86-64: Booting from CD/USB on real hardware is possible, but driver support is limited.
*   AArch64 (ARM64): Has been made to work on some hardware, but setup typically requires significant user effort and code digging.
*   Consult the `user-manual.md` and `README.md` for more specific details on supported chipsets.

**Q: Where can I get help or support?**

A: The primary place for help, support, and to follow development is the #mezzano IRC channel on Libera Chat (irc.libera.chat).

**Q: How do I save my work in Mezzano?**

A: Mezzano uses a "snapshot" feature. This saves the entire current state of your Mezzano system to disk.
To take a snapshot:
1.  Open a REPL (Read-Eval-Print Loop) by pressing `M-F10` (Alt + F10).
2.  Type the command `(mezzano.supervisor:snapshot)` and press Enter.
3.  Wait for the yellow status light at the top-left of the screen to turn off.
When you next boot Mezzano, it will resume from this saved state. See `getting-started.md` or `tutorials.md` for more details.

**Q: What are the "blinkenlights" at the top of the screen?**

A: These are status lights indicating system activity. For a full list and their meanings, please see the "Blinkenlights" section in the `user-manual.md`.

**Q: How do I connect to the internet?**

A: Mezzano has support for networking, primarily with RTL8168 and virtio-net NICs.
*   Network configuration can be viewed via the Network pane of the "Peek" application.
*   The default configuration is often specific to VirtualBox's and QEMU's NAT networks.
*   **Important:** Currently, DHCP is not supported, and bridging to a real network is generally not supported without manual configuration. This means Mezzano might not automatically connect to your local network like other operating systems.

**Q: How do I install new software in Mezzano?**

A: Mezzano has a port of Quicklisp, a Common Lisp library manager. This allows you to download and install many Common Lisp libraries and systems.
*   You can typically load Quicklisp from the REPL.
*   For more information on using Quicklisp within Mezzano, refer to any specific notes in the `user-manual.md` or consult the Mezzano community.
Mezzano does not have a traditional package manager for pre-compiled binary applications like some other operating systems. Software is generally run from source or loaded via Quicklisp.

**Q: How do I quit or shut down Mezzano?**

A: The typical way to "finish" a session is to take a snapshot (see above) and then power off the virtual machine. When you restart, Mezzano will resume from where you left off. There isn't a traditional "shutdown" command that cleans up and powers off in the same way as other operating systems.

**Q: What are some basic applications I can use?**

A: Mezzano comes with several built-in applications. You can usually launch them from the REPL. Some examples include:
*   **Filer:** A file manager.
*   **Editor:** A text editor (Emacs-like keybindings).
*   **Peek:** A system information tool.
*   **Memory Monitor:** To view memory usage.
*   **IRC:** An IRC client.
*   **Telnet:** A Telnet client.
See the `user-manual.md` for more details on these applications and how to launch them.
