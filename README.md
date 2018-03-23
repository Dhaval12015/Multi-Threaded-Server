Objective : A server which can serve multiple user requests simultaneously
using threads for sending and receiving files.

Introduction :

A server with the single thread can serve only one user request at time. So
if multiple users’ request simultaneously then server will serve only one request
at a time and put others in queue. After sending the response of that request,
server will pick another request from the queue. But this is infeasible.For get rid
of that problem we can use multi threaded server.

In multi-threaded server, there are N threads which are running parallel.
When request comes to the server that request is allocated to available thread
from threadpool to execute. While server is busy in serving that request, if
another request comes then that will be served using other thread which runs
parallel to all threads in the system. By using multi-threading concept we can
reduce response time and improve throughput of the server.

We can achieve this by building Thread pool , which contains a fixed
number of threads. The server will only serve client requests equal to the size of
the threadpool simultaneously.

Functionality:

In our code we have five classes named,
1. CLIENTConnection.java
2. FileClient.java
3. FileServer.java
4. Helper.java
5. Main.java.

Now we will discuss about the functionality of every classes.

1. FileServer.java :
FileServer.java will start server on given port number by initialize the size of
Threadpool. It overrides the run() method of Runnable class. In this method
server will accept the incoming connection request from clients and put
sockets into pending list. One more thing it does is to start new thread of
Helper class which is described later.

2. Helper.java :
Helper class will check the thread pool for availability of free slot(thread)
and if there is some request pending in the list then it will remove the first
request in the FIFO (First In First Out) Manner and provide it to the free
thread in the threadpool.

3. FileClient.java :
FileClient.java connects client to the server on given IP and port number. It
establish the inputstream for client inputs and then set outputstream to the
server. It has two method receiveFile() and sendFile().
The receiveFile() method will establish it’s inputstream from server and set
outputstream according to client’s choice. After setup these streams , it
uses buffer of 1 Kb to transfer the file data to destination file. After
transferring data it closes connection to the server.
The sendFile() method will open the file which user wants to upload and
store it’s data in buffer array. After that it sends that data to server by
creating outputstream properly.

4. CLIENTConnection.java :
Whenever server has free thread it assign that thread to pending client
socket by creating CLIENTConnection object. This thread will takes input
from client socket and call appropriate method to serve client request. It
also has two methods sendFile() and receiveFile() as mention above. Here
receiveFile() method will receive the file from client and sendFile() method
sends the file asked by client.

5. Main.java :
It just creates a server thread on specific port number and specifies the size
of threadpool.

The above code creates multithreaded server with functionality of
upload and download files. The client may choose download path while
downloading a file from server.

Conclusion:
We have created a server-client code with multithreaded functionality
which behave almost exactly as the real server except that it runs on the
localhost.
