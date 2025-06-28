# Mezzano Peek Manual

Peek is a system utility that provides a text-based view of various internal system states and information within a graphical window.

## Launching Peek

You can launch Peek from the REPL using the following command:

```lisp
(mezzano.gui.peek:spawn)
```

This will open the Peek window, defaulting to the Help view.

## The Peek Window

The Peek window has a title bar ("Peek") and standard window controls like a close button, and it is resizable. The main area of the window is a text pane where information is displayed.

At the top of the text pane, a header lists the available commands:
`Commands: Help(?) Thread(T) Memory(M) Network(N) CPU(C) Disk(D) Quit(Q)`

## Using Peek - Commands

Peek operates via single-character commands that switch the displayed information panel. Press the character key corresponding to the desired view.

*   **`?` - Help View (`peek-help`)**
    *   This is the default view when Peek starts.
    *   It lists all available commands, their associated character keys, and a brief description of the information they provide.

*   **`T` - Thread View (`peek-thread`)**
    *   Displays a list of all currently active threads in the system.
    *   For each thread, it shows:
        *   Thread Name
        *   State (e.g., `:RUNNING`, `:SLEEPING`, `:STOPPED`)
        *   If a thread is `:SLEEPING`, the item it is waiting on (e.g., a lock, a mailbox) is also displayed.

*   **`M` - Memory View (`peek-memory`)**
    *   Shows detailed memory usage statistics by calling the system's `(room)` function. This typically includes:
        *   Usage of general memory areas.
        *   Cons area usage (for Lisp cons cells).
        *   Pinned and wired area usage.
        *   Function area usage.
        *   Information on free memory, garbage collection, etc.
    *   The output format is textual and provides a snapshot of the system's memory state.

*   **`N` - Network View (`peek-network`)**
    *   Provides a comprehensive overview of the networking subsystem:
        *   **Network Cards (NICs):** Lists each detected network card, its MAC address, assigned IPv4 address and prefix length (if any), and detailed statistics (bytes/packets received/transmitted, errors, collisions).
        *   **Routing Table:** Displays the system's IP routing table, showing network destinations, gateway addresses, prefix lengths, and tags.
        *   **DNS Servers:** Lists the configured DNS servers.
        *   **Listeners:** Shows active TCP listeners (ports open for incoming connections).
        *   **DHCP Leases:** Displays active DHCP leases for each network interface.
        *   **TCPv4 Connections:** Lists all active TCP version 4 connections, including local IP/port, remote IP/port, and connection state (e.g., `ESTABLISHED`, `TIME-WAIT`).
        *   **UDPv4 Connections:** Lists active UDP version 4 connections, showing local IP/port and remote IP/port.

*   **`C` - CPU View (`peek-cpu`)**
    *   Displays detailed information about the system's CPU(s):
        *   Lists each CPU core recognized by the Mezzano supervisor.
        *   CPU vendor string (e.g., "GenuineIntel", "AuthenticAMD").
        *   Maximum supported CPUID levels (standard and extended).
        *   Processor signature: Model, Family, Stepping ID, Processor Type.
        *   Brand Index (if applicable).
        *   CLFLUSH line size.
        *   Local APIC ID.
        *   A list of detected CPU features (e.g., SSE, SSE2, MMX, AVX, NX, LM, etc.), derived from CPUID flags.

*   **`D` - Disk View (`peek-disk`)**
    *   Shows information about all storage disks recognized by the system:
        *   Internal disk object representation and its assigned name (if any, e.g., `SDA`).
        *   Read/write or read-only status.
        *   Sector size in bytes.
        *   Total disk size in sectors and in octets (bytes).
        *   Indicates if a disk is currently used as the paging disk.

*   **`Q` - Quit**
    *   Closes the Peek application window. This can also be achieved by clicking the window's close button.

*   **`Space` - Refresh**
    *   Pressing the Space bar will refresh the content of the currently active view, re-querying the system for the latest information.

Peek is a valuable tool for developers and users to inspect the live state of a Mezzano system. Due to the textual nature of its output, you might need to resize the window to see all information clearly, especially for wider outputs like the Network or CPU views.
