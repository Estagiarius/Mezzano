# Mezzano IRC Client Manual

The Mezzano IRC Client allows you to connect to Internet Relay Chat (IRC) servers, join channels, and communicate with other users.

## Launching the IRC Client

You can launch the IRC Client from the REPL using the following command:

```lisp
(mezzano.irc-client:spawn)
```

This will open the main IRC client window.

## The IRC Client Window

The client window is composed of several parts:

*   **Title Bar:** Displays "IRC" or "IRC - <server_address>" when connected. It includes standard window controls like a close button and is resizable.
*   **Display Pane:** The largest part of the window. This area shows:
    *   Server messages (MOTD, notices, errors).
    *   Channel messages from other users.
    *   Private messages.
    *   Your own messages and actions.
    *   Status messages from the client (e.g., "Connecting to...", "Disconnected...").
*   **Input Pane:** A single-line text entry field at the bottom of the window. This is where you type your messages and commands.
    *   It supports line editing features (like history, using arrow keys) via `*irc-history*`.
    *   The prompt usually indicates the current active channel, e.g., `#channel] ` or just `] ` if no channel is active.
*   **Separator Line:** A thin line separates the display pane from the input pane.

## Getting Started: Basic Workflow

1.  **Set Your Nickname:** Before connecting, you need a nickname.
    ```
    /NICK YourDesiredNick
    ```
    If you don't set one, the client might use a default like "Mezzie" or fail to connect properly.

2.  **Connect to a Server:**
    ```
    /CONNECT server_address
    ```
    *   `server_address` can be a hostname like `irc.libera.chat` or an IP address. You can also use `hostname:port` if the server uses a non-standard port (default is 6667).
    *   The client knows some common servers by name. For example: `/CONNECT LiberaChat` (or just `/CONNECT Libera`). Type `/HELP` to see a list of known servers.
    *   Upon successful connection, you will see server messages, including the Message of the Day (MOTD).

3.  **Join a Channel:**
    ```
    /JOIN #channelname
    ```
    Replace `#channelname` with the actual name of the channel you wish to join (e.g., `/JOIN #mezzano`).
    The first channel you join usually becomes your active channel.

4.  **Send Messages:**
    *   To send a message to the active channel, simply type your message in the input pane and press Enter.
    *   Alternatively, you can use: `/SAY your message here`

5.  **Switch Active Channel (if in multiple channels):**
    ```
    /CHAN #otherchannel
    ```

6.  **Send Private Messages:**
    ```
    /MSG nickname your private message
    ```

7.  **Disconnect:**
    ```
    /DISCONNECT Optional quit message
    ```

8.  **Quit the Client:**
    ```
    /QUIT Optional quit message
    ```
    This will also disconnect you if you are currently connected.

## Commands

Commands are prefixed with a forward slash (`/`). If you type text without a leading `/` and are in an active channel, it's treated as a message to that channel (`/SAY`).

### Connection & Setup
*   **`/CONNECT <server_or_address_or_known_name>`**
    Connects to the specified IRC server. Port defaults to 6667 if not given in `address:port` format.
    Example: `/CONNECT irc.example.com`, `/CONNECT irc.example.com:6697`, `/CONNECT LiberaChat`
*   **`/NICK [new_nickname]`**
    Changes your nickname to `new_nickname`. If `new_nickname` is omitted, displays your current nickname. This command should be used *before* connecting to set your initial nickname.
*   **`/DISCONNECT [message]`**
    Disconnects from the current server with an optional quit `message`.
*   **`/QUIT [message]`**
    Disconnects from the server (if connected) with an optional `message` and closes the IRC client application.

### Channel Operations
*   **`/JOIN <#channel_name> [key]`**
    Joins the specified `channel_name`. If the channel requires a `key` (password), provide it.
*   **`/PART [message]`**
    Leaves the current active channel with an optional `message`.
*   **`/CHAN <#channel_name>`**
    Switches the active context to `channel_name`. You must have already joined this channel. Messages sent with `/SAY` or just by typing will go to this channel.

### Messaging
*   **`/SAY <message_text>`** (or just typing `<message_text>`)
    Sends `message_text` to the current active channel.
*   **`/MSG <target_nick_or_channel> <message_text>`**
    Sends a private `message_text` to `target_nick_or_channel`.
*   **`/ME <action_text>`** (also available as `/ACTION <action_text>`)
    Sends a CTCP ACTION to the current active channel (e.g., `* YourNick performs action_text`).

### Miscellaneous
*   **`/RAW <raw_irc_message>`**
    Sends the `raw_irc_message` directly to the server. For advanced users or debugging.
*   **`/EVAL <lisp_code>`**
    Evaluates the given `lisp_code` within the IRC client's Lisp environment. Results are printed to the display pane. Use with caution.
*   **`/HELP`**
    Displays a list of available client commands and known server names.

## Server Messages

The client will display various messages from the IRC server, including:
*   Welcome messages and MOTD (Message of the Day) upon connection.
*   Replies to your commands (e.g., topic of a channel, user lists).
*   Error messages (e.g., nickname in use, no such channel).
*   Notices from server administrators or services.
*   Other users joining/parting channels, changing nicks, etc.

Many numeric replies from the server are decoded into more readable forms by the client.

## Initialization File

The IRC client will attempt to load an initialization file from `SYS:HOME;IRC-INIT.lisp` when it starts. You can place Lisp code in this file to customize settings, define aliases, or automatically connect to servers. For example, you could set your default nickname:
```lisp
(setf mezzano.irc-client::*default-nick* "MyPreferredNick")
```
Or, more directly if the client instance is accessible or through commands:
```lisp
;; (This would require more complex setup, typically done by interacting with the client object itself
;; or by sending commands after connection if the init file is loaded post-GUI setup but pre-connect logic.)
;; For now, setting *default-nick* is the most straightforward example for an init file.
```

The init file is loaded before the main GUI loop starts, so direct GUI interactions might not be possible from it, but setting variables or defining functions that are later called by commands is feasible.Tool output for `create_file_with_block`:
