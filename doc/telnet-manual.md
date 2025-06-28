# Mezzano Telnet Client Manual

The Mezzano Telnet Client allows you to connect to remote servers using the Telnet protocol. It provides a terminal interface to interact with these servers.

## Launching the Telnet Client

You can launch the Telnet client from the REPL using the `spawn` function:

```lisp
(mezzano.telnet:spawn &key server port terminal-type width height)
```

**Parameters:**

*   `&key server` (String): The hostname or IP address of the Telnet server to connect to.
    *   If an empty string (default) or not provided, the client will prompt you to enter a server address in its terminal window upon launch.
    *   Example: `:server "nethack.alt.org"`
*   `&key port` (Integer): The port number on the server. Defaults to `23`.
    *   Example: `:port 2323`
*   `&key terminal-type` (String): The terminal type string to announce to the server (e.g., for `TERM` environment variable). Defaults to `"xterm-color"`.
    *   Example: `:terminal-type "vt100"`
*   `&key width` (Integer): The initial width of the terminal display in characters. Defaults to `80`.
*   `&key height` (Integer): The initial height of the terminal display in characters. Defaults to `24`.

**Examples:**

*   Launch and prompt for server: `(mezzano.telnet:spawn)`
*   Connect directly to a server: `(mezzano.telnet:spawn :server "mybbs.example.com")`
*   Connect to a server on a specific port with a larger terminal:
    `(mezzano.telnet:spawn :server "server.example.org" :port 7777 :width 100 :height 40)`

## The Telnet Window

*   The client opens a graphical window typically titled "Telnet" or "Telnet - <server_address>:<port>" once connected.
*   The window contains an embedded terminal display, powered by an xterm-like terminal emulator. This handles character display, colors (if negotiated and supported by the server/application), cursor positioning, and basic terminal escape codes.
*   The window is resizable. When resized, the terminal dimensions (character rows/columns) will adjust, and if the server supports NAWS (Negotiate About Window Size), the new dimensions are sent to the server.
*   Standard window controls, like a close button, are present.

## Connecting to a Server

If you launch the client without specifying a `server` argument, it will first display a list of "Known servers" (shortcuts defined within the client, like "nao" for "nethack.alt.org") and then prompt you with:
```
Server>
```
Type the hostname or IP address of the server you wish to connect to and press Enter.

Once a server and port are determined (either from arguments or user input), the client attempts to establish a connection.

## Interaction

*   **Sending Data:** Characters you type into the Telnet window are sent to the remote server.
*   **Receiving Data:** Data received from the server is displayed in the terminal window. This includes text output from remote applications, prompts, etc.
*   **Terminal Emulation:** The client relies on its underlying xterm widget to interpret most terminal control codes sent by the server for formatting output, moving the cursor, etc.
*   **Line Endings:** The client handles CR (Carriage Return) and CR NUL sequences appropriately for display.

## Telnet Protocol Features

The client implements several aspects of the Telnet protocol:

*   **Command Interpretation (IAC):** Correctly processes Interpret As Command (IAC) sequences.
*   **Option Negotiation:** It will attempt to negotiate the following options with the server:
    *   **Suppress Go-Ahead (`+option-suppress-go-ahead+`):** The client indicates it WILL suppress go-ahead, and prefers the server to DO the same.
    *   **Terminal Type (`+option-terminal-type+`):** If the server requests (DO), the client will respond with its configured terminal type (e.g., "xterm-color").
    *   **Window Size (NAWS - `+option-window-size+`):** The client indicates it WILL send window size information. If the server agrees (DO), the client will send updates when its window is resized.
*   It will generally refuse (WONT) other options it doesn't explicitly support.

## Disconnecting

*   To disconnect from the server, you typically use the logout command of the remote system you are connected to (e.g., `exit`, `logout`, `bye`).
*   If the server closes the connection, the Telnet client will display a "Disconnected from server" message.
*   Closing the Telnet window using the window's close button will also terminate the connection and the application.

## Notes and Limitations

*   **Character Encoding:** The documentation notes a FIXME regarding UTF-8 translation. While Mezzano itself handles Unicode, the Telnet client's direct byte handling for network I/O and passthrough to the xterm widget might have implications for full UTF-8 correctness in all scenarios with all servers.
*   **Advanced Telnet Options:** The client supports common options like terminal type and window size but may not support more esoteric Telnet options.
*   The actual terminal emulation capabilities (e.g., specific escape sequences supported, color fidelity) depend on the `mezzano.gui.xterm:xterm-terminal` component.
