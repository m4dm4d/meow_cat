#meow_cat

A lightweight **Netcat-like TCP networking tool written from scratch in Python**.

This project was built as a learning exercise to understand how tools such as Netcat work internally, while practicing **TCP socket programming, client-server architecture, threading, command execution, file transfer, and Python CLI development**.

> **Disclaimer:** This project is intended for educational purposes, CTFs, networking experimentation, and authorized security testing only. Do not use it against systems or networks without explicit permission.

---

## Features

* TCP client mode
* TCP listener/server mode
* Interactive command shell
* Remote command execution
* File upload
* Multiple client handling using Python threads
* IPv4 socket communication
* Command-line argument parsing with `argparse`
* Basic `Ctrl+C` handling
* Configurable target IP and TCP port

---

## How It Works

The program implements a basic TCP client/server architecture.

### Client Mode

In client mode, the program connects to a specified target and port using a TCP socket.

```text
┌──────────────┐                 ┌──────────────┐
│    Client    │ ───── TCP ────>│    Server    │
│              │                 │              │
│   connect()  │                 │   listen()   │
│   send()     │                 │   accept()   │
│   recv()     │                 │   recv()     │
└──────────────┘                 └──────────────┘
```

### Listener Mode

In listener mode, the program:

1. Creates a TCP socket.
2. Binds it to the specified IP and port.
3. Starts listening for connections.
4. Accepts incoming clients.
5. Creates a separate thread to handle each client.

## The implementation uses `bind()`, `listen()`, and `accept()` for the server side and `connect()` for the client side.

## Requirements

* Python 3
* Linux/macOS/Windows with Python 3
* No external Python packages are required

The project uses Python's standard library modules:

```text
argparse
socket
shlex
subprocess
sys
textwrap
threading
```

---

## Installation

Clone the repository:

```bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_DIRECTORY>
```

No additional dependencies are required.

Check that Python is installed:

```bash
python3 --version
```

---

## Usage

Display the help menu:

```bash
python3 nc.py -h
```

Available options:

| Option            | Description                           |
| ----------------- | ------------------------------------- |
| `-t`, `--target`  | Target IP address / listening address |
| `-p`, `--port`    | TCP port                              |
| `-l`, `--listen`  | Start listener mode                   |
| `-c`, `--command` | Enable interactive command shell      |
| `-e`, `--execute` | Execute a specified command           |
| `-u`, `--upload`  | Receive and save a file               |

These options are implemented using Python's `argparse` module.

---

## Examples

### 1. Start a Command Shell Listener

Start the server:

```bash
python3 nc.py -t 0.0.0.0 -p 5000 -l -c
```

Then connect from another authorized machine or terminal:

```bash
nc <SERVER_IP> 5000
```

The server provides an interactive command interface.

---

### 2. Execute a Specific Command

The `-e` option allows a listener to execute a specified command when a client connects.

Example:

```bash
python3 nc.py -t 0.0.0.0 -p 5000 -l -e "whoami"
```

The command is processed through the program's command execution function.

---

### 3. Receive a File

The listener can receive data from a client and save it to a specified file:

```bash
python3 nc.py -t 0.0.0.0 -p 5000 -l -u received.txt
```

The server collects incoming data and writes it to the specified file.

---

## Project Structure

The project currently consists primarily of:

```text
.
├── nc.py
└── README.md
```

The main components of `nc.py` are:

```text
NetCat
 ├── run()
 ├── send()
 ├── listen()
 └── handle()

execute()
```

### `NetCat`

The `NetCat` class handles the TCP networking functionality.

### `send()`

Responsible for client-side TCP connections and exchanging data with the server.

### `listen()`

Creates the listener, accepts incoming connections, and starts a new thread for each client.

### `handle()`

Handles individual clients and provides the different server-side functionalities:

* Command execution
* File upload
* Interactive command shell

### `execute()`

Uses Python's `subprocess` module to execute commands and return their output.

---

## What I Learned

I built this project primarily to understand networking concepts by implementing them myself instead of relying entirely on existing tools.

Through this project, I practiced:

* TCP/IP fundamentals
* Python socket programming
* Client-server architecture
* `socket.connect()`
* `socket.bind()`
* `socket.listen()`
* `socket.accept()`
* `socket.send()`
* `socket.recv()`
* Multi-client handling with Python threads
* Command-line argument parsing with `argparse`
* Working with bytes and strings
* Python `subprocess`
* Basic file transfer over TCP
* Exception handling
* Debugging Python execution and networking errors

---

## Development Journey

This project also helped me understand several practical problems that don't always become obvious when learning Python syntax alone.

For example, I had to debug:

* Python indentation errors
* Incorrect `argparse` flag definitions
* The difference between arguments that require values and boolean flags
* Python class definition order
* TCP `bind()` errors
* Incorrect IP/interface selection
* Connection refused errors
* Client mode vs listener mode

This made the project useful not only as a networking exercise, but also as a practical debugging exercise.

---

## Current Limitations

This is an educational implementation and is **not intended to replace Netcat or other mature networking utilities**.

Some areas that could be improved include:

* More robust error handling
* Better connection management
* Improved file-transfer protocol
* Better handling of client disconnections
* More robust command parsing
* Logging
* Connection timeouts
* Authentication
* Encrypted communication
* UDP support
* Improved protocol design

---

## Future Improvements

Possible future additions:

* [ ] UDP support
* [ ] Connection timeout options
* [ ] Improved error handling
* [ ] Better file-transfer protocol
* [ ] Authentication
* [ ] TLS encryption
* [ ] Connection logging
* [ ] Improved client disconnect handling
* [ ] Better command parsing
* [ ] More robust multi-client management
* [ ] Interactive session improvements

---

## Technologies

```text
Python 3
TCP/IP
IPv4
Python socket
argparse
threading
subprocess
```

---

## Educational Purpose

The main goal of this project is to understand what happens underneath a simple network utility.

Instead of only using:

```bash
nc <IP> <PORT>
```

the goal was to understand how a program can implement the underlying concepts using Python:

```text
Socket
   ↓
TCP Connection
   ↓
Client / Server
   ↓
Data Exchange
   ↓
Threading
   ↓
Command / File Handling
```

---

## Disclaimer

This software can perform network communication and execute commands on the system where it is running.

Use it **only on systems and networks that you own or have explicit permission to test**.

The author is not responsible for misuse of this software.

---

## Author

**Aryaneel Das**

Cybersecurity enthusiast | CTF Player | Python & Linux

Interested in:

* Cybersecurity
* Penetration Testing
* Network Security
* Cryptography
* Reverse Engineering
* CTFs
* Python
