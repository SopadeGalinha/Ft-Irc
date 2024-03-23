# <h1 align="center">FT-IRC (Internet Relay Chat)</h1>

## About the project
Internet Relay Chat (IRC) is a protocol for real-time text communication over the Internet. Developed by **Jarkko Oikarinen** in Finland, IRC allows users to join channels, which are essentially chat rooms dedicated to specific topics. Within these channels, users can engage in live discussions with people from around the world. IRC follows a client-server model, requiring both client and server software for operation. Various IRC clients are available for different platforms, including PC, Macintosh, and UNIX systems.

<div style="text-align:center">
    <img src="https://github.com/SopadeGalinha/Ft-Irc/raw/main/assets/75684404/5645e3c6-69ec-4c31-8515-19ec18f06080.png" alt="irc_architecture1">
</div>

### Advantages of IRC:
- Decentralization: IRC is decentralized, meaning it does not rely on a single central server for operation. This decentralization contributes to its resilience and longevity.
- Chat and file sharing: IRC supports not only text communication but also file sharing, allowing users to exchange files within channels or through private messages.
- Real-time discussion: IRC facilitates real-time discussions, making it suitable for quick exchanges and collaborative work.
- Access levels: IRC allows users to set access levels, providing better privacy and control over who can participate in conversations.

### Disadvantages of IRC:
- Bandwidth consumption: IRC can consume significant bandwidth, which may be a concern for users with limited data plans or slow connections.
- Flooding: The open nature of IRC channels leaves them susceptible to flooding, where users flood the channel with excessive messages, disrupting communication.
- Security incidents: IRC networks are not immune to security incidents, including attacks such as DDoS (Distributed Denial of Service) attacks or exploits targeting IRC software vulnerabilities.

## Project requirements

### Development Specifications
- Develop an IRC server in C++ 98.
- Do not develop a client.
- Do not handle server-to-server communication.
- Executable usage: `./ircserv <port> <password>`
  - `<port>`: Port number for incoming IRC connections.
  - `<password>`: Connection password required by any IRC client.
- Server must handle multiple clients simultaneously without hanging.
- Forking is not allowed; all I/O operations must be non-blocking.
- Only 1 `poll()` (or equivalent) can be used for handling all operations (read, write, listen, etc.).

### Reference Client
- Choose one IRC client as a reference.
- Reference client must connect to the server without errors.
- Communication between client and server via TCP/IP (v4 or v6).
- Using reference client with the server should resemble usage with official IRC servers.

### Implemented Features
- Authentication, nickname setting, username setting, channel joining, sending and receiving private messages.
- Forward messages from one client to every other client in the channel.
- Implement operators and regular users.
- Implement specific commands for channel operators:
  - KICK: Eject a client from the channel.
  - INVITE: Invite a client to a channel.
  - TOPIC: Change or view the channel topic.
  - MODE: Change the channel's mode:
    - i: Set/remove Invite-only channel.
    - t: Set/remove restrictions of the TOPIC command to channel operators.
    - k: Set/remove the channel key (password).
    - o: Give/take channel operator privilege.
    - l: Set/remove the user limit to the channel.


## Test Example

To verify that the server correctly processes every possible error and issue, including receiving partial data and low bandwidth, follow the steps below:

1. Start the server.
2. Open a terminal window and run the following command to connect to the server using `nc`:
```sh
$ nc 127.0.0.1 6667
```
3. Use Ctrl+D to send the command in several parts:
- Type `'com'`, then press Ctrl+D.
- Type `'man'`, then press Ctrl+D.
- Type `'d\n'`, then press Ctrl+D.
4. Observe the server's response to ensure it correctly processes the aggregated packets and executes the command.

This test ensures that the server handles partial data and processes commands accurately by aggregating received packets to rebuild the command.

## Resources
[Internet Relay Chat](https://chi.cs.uchicago.edu/chirc/irc.html) - Overview of IRC





