# Google-File-System
Implementing Google File System in Python 3

### How to Run :
- In one terminal, run **python3 Master_Server.py** to start master server.
- In other terminal, run **python3 Chunk_Server.py** to start chunk servers.
- From the third terminal, run **python3 Client.py**.

### Syntax :
To run the Master Server : 
```sh
python3 Master_Server.py
```
To run the BackUp Master Server : 
```sh
python3 Backup_Master_Server.py
```
To run the chunkserver [All the chunkservers to be run with their port numbers] : 
```sh
python3 Chunk_Server.py port_number(of chunkservers)
```
To run the client :
```sh
python3 Client.py
```

### Commands in client:
- **upload file_name** : To upload the file into the chunkservers.
- **download file_name** : To download the file from the chunkservers.
- **lease file_name** : Put a lease/lock on the file,so that no other client can upload/download the file.
**unlease file_name** : Remove the lease put on the file.

### Architecture:
- One Master Server
- One BackUp Master Server
- Four Chunkservers
- Multiple Clients Allowed

### Features:
- A single file of client will be divided into chunks and **each chunk will be stored in seperate chunk servers**.
- There will also be **3 duplicate replicas for each chunk of a file** which will be stored in seperate chunk servers. This is done so as to **increase data availablity** to the client.
- **Master Server will only hold the Metadata of all the chunks of the files** which will be used by clients and chunkservers to communicate with the appropriate chunkserver. Hence there is no issue of Master Server being overloaded.
- As **Master Server is a single point of failure, hence we have a Backup Master Server making the system more reliable**.
- A **log_file.txt** will also be maintained which would store history of all operations. **This log file can be used by Master Server to recover to current state after failure**.
- To check the list of active chunk servers, **a thread is created in the Master Server which after every 6 seconds will try to connect to all 4 chunk servers and display list of active chunkservers out of them.**

### Miscellaneous Details:
- constants.py contains common metadata including port numbers of master server, chunk servers, etc.
- Proper logging is provided in each of chunk server, master server and client.
- Most of the errors are handled in the code.
- As per original GFS, files are identified by absolute paths. There is no concept of directories. GFS has a module which keeps checks on file path and directory structure consistencies. It is not implemented here.
- The code is gradually extendable by adding features one by one.

