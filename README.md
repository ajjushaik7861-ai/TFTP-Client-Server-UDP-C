# TFTP Client-Server File Transfer Using UDP in C

## Project Overview

This project implements the **Trivial File Transfer Protocol (TFTP)** using the **UDP protocol** in C on Linux. It provides a lightweight client-server application capable of transferring files between two systems using block-based communication and acknowledgements.

The project follows the basic TFTP protocol defined in RFC 1350 and demonstrates socket programming, file handling, packet-based communication, and reliable data transfer over UDP.

---

## Features

- Upload files from Client to Server (PUT)
- Download files from Server to Client (GET)
- UDP Socket Programming
- Stop-and-Wait Protocol
- 512-byte Block Data Transfer
- Acknowledgement (ACK) for every DATA packet
- Three transfer modes
  - Normal Mode
  - Octet Mode (Binary Transfer)
  - Netascii Mode (ASCII Text Transfer)
- Error Handling
- Interactive Command-Line Interface

---

## Technologies Used

- Language : C
- Operating System : Linux (Ubuntu / WSL)
- Network Protocol : UDP
- Compiler : GCC
- APIs : POSIX Socket APIs

---

## Project Structure

```
TFTP Project
│
├── client
│   ├── tftp_client.c
│   ├── tftp.c
│   ├── tftp.h
│   └── tftp_client.h
│
├── server
│   ├── tftp_server.c
│   ├── tftp.c
│   └── tftp.h
│
└── README.md
```

---

## TFTP Packet Format

### Request Packet (RRQ / WRQ)

```
------------------------------------------------
| Opcode (2 Bytes) | Filename | Mode |
------------------------------------------------
```

### Data Packet

```
-----------------------------------------
| Opcode | Block Number | Data (512B) |
-----------------------------------------
```

### ACK Packet

```
-------------------------------
| Opcode | Block Number |
-------------------------------
```

### ERROR Packet

```
----------------------------------------
| Opcode | Error Code | Error Message |
----------------------------------------
```

---

## TFTP Operation Codes

| Opcode | Meaning |
|---------|---------|
| 1 | RRQ (Read Request) |
| 2 | WRQ (Write Request) |
| 3 | DATA |
| 4 | ACK |
| 5 | ERROR |

---

## Working Principle

### PUT Operation

```
Client
   |
   | WRQ
   |
Server
   |
   | ACK
   |
Client
   |
   | DATA Block 1
   |
Server
   |
   | ACK Block 1
   |
Client
   |
   | DATA Block 2
   |
Server
   |
   | ACK Block 2
```

The process continues until the final data block is smaller than the configured block size.

---

### GET Operation

```
Client
   |
   | RRQ
   |
Server
   |
   | ACK
   |
Server
   |
   | DATA Block 1
   |
Client
   |
   | ACK Block 1
   |
Server
   |
   | DATA Block 2
   |
Client
   |
   | ACK Block 2
```

---

## Transfer Modes

### Normal Mode

- Transfers 512 bytes per packet.
- Best for normal file transfers.

### Octet Mode

- Transfers binary data.
- Sends one byte at a time.
- Suitable for binary files.

### Netascii Mode

- Text transfer mode.
- Converts newline (`\n`) into carriage return + line feed (`\r\n`).

---

## Compilation

### Server

```bash
cd server
gcc tftp_server.c tftp.c -o server
./server
```

### Client

```bash
cd client
gcc tftp_client.c tftp.c -o client
./client
```

---

## Client Commands

```
connect
```

Connect to the server.

```
get
```

Download a file from the server.

```
put
```

Upload a file to the server.

```
mode
```

Change transfer mode.

```
exit
```

Disconnect from the server.

---

## Sample Execution

### Server

```
TFTP Server listening on port 6969...

READY TO RECEIVE

Received block 1
Received block 2

FILE RECEIVED SUCCESSFULLY
```

### Client

```
TFTP Menu

connect
put
mode

READY TO SEND

Sent block 1
Sent block 2

FILE SENT SUCCESSFULLY
```

---

## Socket APIs Used

- socket()
- bind()
- sendto()
- recvfrom()
- close()

---

## File APIs Used

- open()
- read()
- write()
- close()
- lseek()
- unlink()

---

## Concepts Learned

- UDP Socket Programming
- Client-Server Architecture
- Reliable File Transfer
- Stop-and-Wait Protocol
- Packet Design
- Socket Address Structures
- File Handling in Linux
- POSIX System Calls
- Error Handling
- Network Programming

---

## Future Enhancements

- Timeout and Retransmission
- Multi-client Support
- Thread-based Server
- Progress Bar
- File Integrity Verification (CRC)
- IPv6 Support
- Secure File Transfer
- Logging System

---

## Author

**Md Abdul Azeez**

Embedded Systems Engineer

### Skills

- C
- Embedded C
- Linux
- Socket Programming
- UDP/TCP
- CAN
- UART
- I2C
- SPI
- RTOS
- PIC18F4580
- Data Structure
