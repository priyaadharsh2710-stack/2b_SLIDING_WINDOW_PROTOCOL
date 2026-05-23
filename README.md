# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM

To simulate the Sliding Window Protocol using Python socket programming for transmitting frames between client and server with acknowledgements.

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
Client:
```
import socket

s = socket.socket()

s.connect(('localhost', 8000))

n = int(input("Enter number of frames: "))

w = int(input("Enter window size: "))

frames = list(range(1, n + 1))

i = 0

while i < n:

    send_frames = frames[i:i + w]

    msg = " ".join(map(str, send_frames))

    print("Sending frames:", msg)

    s.send(msg.encode())

    ack = s.recv(1024).decode()

    print("Received:", ack)

    i += w

s.close()
```
Server:
```
import socket

host = 'localhost'
port = 8000

server_socket = socket.socket()

server_socket.bind((host, port))

server_socket.listen(1)

print("Server listening...")

conn, addr = server_socket.accept()

print("Connected by", addr)

while True:

    data = conn.recv(1024)

    if not data:
        break

    msg = data.decode()

    print("Received frames:", msg)

    ack = "ACK for frames: " + msg

    conn.send(ack.encode())

conn.close()
server_socket.close()

```

## OUPUT
<img width="999" height="243" alt="Screenshot 2026-05-23 192958" src="https://github.com/user-attachments/assets/5bf920b1-1932-42de-9f40-6e1ddf0b6c42" />
<img width="972" height="361" alt="Screenshot 2026-05-23 193014" src="https://github.com/user-attachments/assets/85a3b421-4fd6-45a6-b5a3-c1f6b1c067da" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
