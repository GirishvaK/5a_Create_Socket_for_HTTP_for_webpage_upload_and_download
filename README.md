# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.

2.Create a socket using Python socket library.

3.Bind the socket to localhost and port 8080.

4.Listen and accept connection from the client.

5.Receive HTTP request from the client.

6.If the request is GET, read the webpage file and send it to the client.

7.If the request is POST, receive the uploaded data and store it in a file.

8.Send HTTP response to the client.

9.Close the connection.

10.Stop the program.

## Program
Server
```
import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```
Client
```
    import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
## OUTPUT
1.Download

Server

<img width="580" height="196" alt="image" src="https://github.com/user-attachments/assets/e2afccce-6917-4819-baf2-2991cc7a0080" />

Client

<img width="653" height="849" alt="image" src="https://github.com/user-attachments/assets/09e1a84e-9806-4177-a790-2fde84bd609b" />

Excecution

<img width="1909" height="1011" alt="image" src="https://github.com/user-attachments/assets/416df394-bd40-4a51-a60d-0de1b9e6a568" />


2.Upload

Server

<img width="612" height="256" alt="image" src="https://github.com/user-attachments/assets/a59d6be4-aa3e-4120-957f-02a50a5b9d82" />

Client

<img width="579" height="206" alt="image" src="https://github.com/user-attachments/assets/1a1f17fc-03d9-4cc8-b073-3c0b89cf01e1" />

Excecution

<img width="1909" height="1014" alt="image" src="https://github.com/user-attachments/assets/975bf6cc-0863-47a3-914d-3b8b15456559" />


## Result
Thus the socket for HTTP for web page upload and download created and Executed
