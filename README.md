## Programming Project: TCP Sockets

### [Introduction](#intro-anchor)

This is going to be a 2 part project. Part I is just a gentle introduction into
HTTP and TCP. Part II is writing your own web server.

### [Part I: Act like a browser, think like a hacker.](#part1-anchor)

When you use the web, you typically do so in a browser or an app of some kind.
Underneath that pretty user interface, there are many protocols in use.

Namely, Ethernet, IP, TCP, and HTTP.

These protocols are part of the so-called layers of the Internet.

We are going to focus on HTTP for now. When you go to a web page in your browser
what is happening? How does the server you are visiting: Facebook, CNN, GitHub,
etc. know what you want?

It knows because of the HTTP protocol. A protocol is just a way in which two or more parties communicate. In the case of computers, these two "parties" are software programs.

Generally speaking, this is the client/server architecture of the web. There is a client, who wants to get data and the server who sends data to the client.

![Client Server Diagram](/img/clientserver.png)

The HTTP protocol is pretty simple. Protocols like HTTP are much like the protocols
those we use in our everyday life. For example, this morning I bought
my coffee from dingy looking cart few blocks from my apartment:

* ME: I want a large coffee with milk.
* COFFEE GUY: (Hands me a large coffee with milk.)

Okay, this is basically how HTTP works. I'm not kidding. Let's make my morning
coffee routine slightly more "computer like".

* ME: ```GET: Coffee/large/milk/```
* COFFEE GUY:  ```Hands me a large coffee with milk.```

Okay, not a very friendly exchange, but there's a point! Let's look at what an actual
HTTP request looks like.

Your web browser makes an HTTP request that looks like this:
```
GET /index.html HTTP/1.1\n\n
```
The web server:  Returns the web page

So, let's break that down:

```GET``` - this says what it sounds like, GET the page!

```/index.html``` -  this is the file we are asking the web server for.

```HTTP/1.1\n\n``` - this is the only scary-ish part. ```HTTP/1.1``` is the "version" of the
HTTP language we are speaking and the ```\n\n``` are what are called newline characters
which signal that the request we are making is finished.

Don't believe me? Fine, let's just try it. We're going to talk to a web
server in it's "native language" (HTTP) using a program called Telnet. Telnet is kind
of a "raw" way of communicating over a network using sockets and TCP (more on sockets
later--be sure to watch the lectures from Week 6 on TCP).

Use Telnet:

Telnet on Mac OS X:
http://www.wikihow.com/Use-Telnet-on-Mac-OS-X

Telnet on Windows:
https://kb.ctera.com/article/how-to-open-a-telnet-session-on-windows-7-or-windows-8-os-16.html

Okay, once you've gotten telnet up and running on your computer, you should be able to open your Terminal (Mac OS X) or CMD app (Windows) and type the following (the $ character is part of the shell 'prompt' you do not type it):

```
$ telnet www.google.com
Trying 172.217.4.36...
Connected to www.google.com.
Escape character is '^]'.
GET / HTTP/1.1
```
* Press RETURN twice (this us sending those ```\n\n``` characters)

* What do you see?

What about trying this:

```
$ telnet www.google.com
Trying 172.217.4.36...
Connected to www.google.com.
Escape character is '^]'.
GET /maps HTTP/1.1
```

* What do you see now?

Try the same thing on some other websites.

So, that is essentially how HTTP works. Admittedly, this is an oversimplification, but this is the essence of the protocol.

### Part II: BYOWS: (aka) Build Your Own Web Server

What is a web server. Well, a web server is in its simplest form a program that serves web pages to web browsers! More specifically, when your browser visits a website, it is asking the web server for a particular file. Much like we did in Part 1, the web server is responding to GET requests so that the browser can download a file and display it in your browser. Remember, a web page is HTML contained in a file that your web browser "renders".

### How does a socket work?

A socket is a software abstraction that allows you to connect two pieces of
software over a network. These two pieces of software are usually
running on two different devices. e.g. your phone's web browser and a web server on the Internet.

You can think of sockets like the two ends of a pipe. When you want to connect to a web server, your device begins a connection setup process that, if successful, results in the a virtual "pipe" being constructed between you and the server in question.

When you connect to a website your browser **creates** a socket and **connects** to
the web server in question.

The web server you are connecting  also has a socket already **listening**
for connections. When it "hears" you connecting, it makes a connection back to
you and then you can both begin to communicate with one another over this
connection.

![Pipe Diagram](/img/pipe.png)

When I say "abstraction" I mean that "under the hood" there is more
going on than would appear on the surface.

In the same way that the gas pedal on a car is an abstraction that makes our car
"go faster" when we press it.

A socket is really a software abstraction and "under the hood" TCP is being
used to transmit data between you and your destination. This allows for the reliable transfer of data over the Internet. Remember, you will learn that the the Internet, that is the IP protocol, is inherently unreliable. That is, it can "drop" or lose packets. TCP is used to ensure that data can be delivered reliably in spite of this.


### Getting Started with the Python Socket Library

Your program will be the server. As such, there are 5 steps to creating a socket that can handle client requests. See the code excerpts below.

```python
# 1. Create a socket
my_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 2. "Bind" the socket to an IP and PORT
my_socket.bind((host, port))

# 3. Begin "listening" on the socket
my_socket.listen(5)

# 4. Begin "accepting" client connections
conn, addr = sock.accept()
```

![Socket Diagram](/img/server.png)

### Requirements

You are going to write two programs.
In part I, you will write a client program.

In part II, you will modify your client program slightly and write a server
program. You will then be able to use these two to communicate with one another
using the console.

### Language

The assignment should be done using Python. If you want to use something else, come talk to me first.

### Running your program

You should run your two programs like so:

```
python simple_server.py 3000

```
Where ```3000``` is the port you are running your server on.

### Additional Resources

Sockets:

https://docs.python.org/3/howto/sockets.html
https://docs.python.org/2/howto/sockets.html

### Academic Integrity

It is imperative that you do not copy and paste code from the Internet, books, or elsewhere.

If you do, we will be able to tell. Don't do it.

This does not mean that you can't research the ways other people have tackled a particularly programming problem or look at other code. It means you cannot plagiarize code in the same way you wouldn't for an essay. If you are using a particular Internet resource, StackOverflow, etc., please cite it in your submission.

If you are at a point where the assignment feels completely overwhelming or you are at a loss as to what to do, talk to or email me. I will help you!

https://www.purchase.edu/Policies/academicintegrity.aspx
