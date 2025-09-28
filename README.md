# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
# CLIENT:
```
import socket
c = socket.socket()
c.connect(('localhost', 6000))

while True:
    mac = input("Enter MAC address to find IP (or type 'exit' to quit): ")
    if mac.lower() == "exit":  
        break
    c.send(mac.encode())
    ip = c.recv(1024).decode()
    print(f"IP Address for {mac}: {ip}")
c.close()


```

# SERVER:

```
import socket
s=socket.socket()
s.bind(('localhost',5000))
s.listen(5)
c,addr=s.accept()
address={"165.165.80.80":"68:34:21:83:A9:CD","165.165.79.1":"8A:BC:E3:FA"}
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
## OUPUT - ARP
<img width="936" height="498" alt="image" src="https://github.com/user-attachments/assets/039a921e-5ea5-4c01-ae87-d1e6e0f8c759" />

## PROGRAM - RARP
# CLIENT:

```
import socket
c = socket.socket()
c.connect(('localhost', 6000))

while True:
    mac = input("Enter MAC address to find IP (or type 'exit' to quit): ")
    if mac.lower() == "exit":  
        break
    c.send(mac.encode())
    ip = c.recv(1024).decode()
    print(f"IP Address for {mac}: {ip}")
c.close()
```

# SERVER:

```
import socket
s = socket.socket()
s.bind(('localhost', 6000))
s.listen(5)
print("Server is listening for RARP requests...")
c, addr = s.accept()
print(f"Connection established with {addr}")

rarp_table = {
    "6A:08:AA:C2": "165.165.80.80",
    "8A:BC:E3:FA": "165.165.79.1"
}

while True:
    mac = c.recv(1024).decode()

    if not mac:  
        break

    try:
        ip = rarp_table[mac]  
        print(f"MAC: {mac} -> IP: {ip}")
        c.send(ip.encode())  
    except KeyError:
        print(f"MAC: {mac} not found in RARP table.")
        c.send("Not Found".encode())
c.close()
s.close()

```
## OUPUT -RARP
<img width="1251" height="223" alt="image" src="https://github.com/user-attachments/assets/ea5df3e5-3238-46ec-91f2-baafaa22547c" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
