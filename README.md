# <h1 align="center">FT-IRC (Internet Relay Chat)</h1>

## About the project
Internet Relay Chat (IRC) is a protocol for real-time text communication over the Internet. Developed by **Jarkko Oikarinen** in Finland, IRC allows users to join channels, which are essentially chat rooms dedicated to specific topics. Within these channels, users can engage in live discussions with people from around the world. IRC follows a client-server model, requiring both client and server software for operation. Various IRC clients are available for different platforms, including PC, Macintosh, and UNIX systems.

### Advantages of IRC:
- Decentralization: IRC is decentralized, meaning it does not rely on a single central server for operation. This decentralization contributes to its resilience and longevity.
- Chat and file sharing: IRC supports not only text communication but also file sharing, allowing users to exchange files within channels or through private messages.
- Real-time discussion: IRC facilitates real-time discussions, making it suitable for quick exchanges and collaborative work.
- Access levels: IRC allows users to set access levels, providing better privacy and control over who can participate in conversations.

### Disadvantages of IRC:
- Bandwidth consumption: IRC can consume significant bandwidth, which may be a concern for users with limited data plans or slow connections.
- Flooding: The open nature of IRC channels leaves them susceptible to flooding, where users flood the channel with excessive messages, disrupting communication.
- Security incidents: IRC networks are not immune to security incidents, including attacks such as DDoS (Distributed Denial of Service) attacks or exploits targeting IRC software vulnerabilities.

<p align="center">
  <img src="https://github.com/SopadeGalinha/Ft-Irc/blob/main/assets/irc_architecture1.png" alt="irc_architecture1">
</p>

The architecture of IRC, as depicted in the figure above, is refreshingly straightforward. At its core, a single IRC server serves as the hub for connections from multiple IRC clients. Each client connects to the server with a unique identity, typically denoted by a distinct nickname, This ensures individuality within the network. Once linked, clients can engage in direct one-on-one conversations with fellow users and execute commands to query the server's status, such as retrieving a list of connected users or acquiring further details about a specific nickname.

Furthermore, IRC facilitates the creation of chat rooms, referred to as channels, fostering one-to-many communication. Users can seamlessly join these channels, where they can share messages with the entire audience. Consequently, these messages reach all users currently present in the channel, enriching collaborative interactions within the IRC network.

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
  - **KICK**: Eject a client from the channel.
  - **INVITE**: Invite a client to a channel.
  - **TOPIC**: Change or view the channel topic.
  - **MODE**: Change the channel's mode:
    - **i**: Set/remove Invite-only channel.
    - **t**: Set/remove restrictions of the TOPIC command to channel operators.
    - **k**: Set/remove the channel key (password).
    - **o**: Give/take channel operator privilege.
    - **l**: Set/remove the user limit to the channel.


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

## TCP/IP

TCP/IP is a suite of communication protocols used for transmitting data over networks, including the Internet. It provides a standardized set of rules and procedures that govern how devices communicate with each other. Key components of TCP/IP include:

- **Transmission Control Protocol (TCP)**: A connection-oriented protocol that ensures reliable and ordered delivery of data packets between devices. TCP establishes and maintains virtual connections between sender and receiver.

- **Internet Protocol (IP)**: A network-layer protocol responsible for addressing and routing packets across interconnected networks. IP assigns unique IP addresses to devices and determines the best path for data transmission.

- **Other Protocols**: TCP/IP encompasses several other protocols, including UDP (User Datagram Protocol), ICMP (Internet Control Message Protocol), and ARP (Address Resolution Protocol), each serving specific purposes within the communication process.

## Sockets

In IRC, sockets play a crucial role in facilitating communication between clients and servers. Here's a brief overview of how sockets are used in IRC:

1. **Server-Side Sockets**: IRC servers listen for incoming connections from IRC clients on a specific port. When a client wants to connect to the IRC server, it initiates a TCP connection to the server's IP address and port. The server accepts incoming connections on this socket.

2. **Client-Side Sockets**: IRC clients create a socket to connect to the server. Once connected, the client can send and receive messages to and from the server using this socket.

3. **Communication Protocol**: IRC communication typically occurs over TCP/IP sockets. Messages between clients and servers are sent as plain text, following the IRC protocol specifications. The server processes incoming messages from clients and broadcasts them to other clients in the appropriate channels.

4. **Socket Operations**: Both the IRC server and client perform socket operations such as opening a socket, establishing a connection, sending data, receiving data, and closing the connection as needed.

5. **Handling Multiple Connections**: IRC servers must handle multiple client connections simultaneously. This is often achieved using techniques like multi-threading or asynchronous I/O to manage concurrent connections efficiently.

Overall, sockets form the backbone of communication in IRC, enabling real-time text-based messaging between clients and servers over the Internet.

## Resources
[Internet Relay Chat](https://chi.cs.uchicago.edu/chirc/irc.html) - IRC Overview <br>
[IRC Communications](https://chi.cs.uchicago.edu/chirc/irc_examples.html) - Exemples of a conversation between an IRC client and server <br>
[RFC2810](https://datatracker.ietf.org/doc/html/rfc2810) - Internet Relay Chat: Architecture <br>





