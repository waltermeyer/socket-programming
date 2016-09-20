## Programming Project: TCP Sockets

## Introduction

This is going to be a 3 part project. Part I is just a gentle introduction into
HTTP and TCP. Part II is programming your own simple text based web browser client.
And Part III is writing a simple web server application.

### Part I: Act like a browser, think like a hacker.

When you use the web, you typically do so in a browser or an app of some kind.
Underneath that pretty user interface, there are many protocols in use.

Ethernet, IP, TCP, HTTP

We are going to focus on HTTP for now. When you go to a web page in your browser
what is happening? How does the server you are visiting--Facebook, CNN, GitHub,
etc. know what you want? It knows because of the HTTP protocol. A protocol

The HTTP protocol is pretty simple. Protocols like HTTP are much like the protocols
those we use in our everyday life. For example, this morning (and every morning) I buy
my coffee from dingy looking cart few blocks from my apartment:

Me: I want a large coffee with milk.
Coffee Guy: Hands me a large coffee with milk.

Okay, this is basically how HTTP works. I'm not kidding. Let's make my morning
coffee routine slightly more "computer like".

Me: GET: Coffee/large/milk/
Coffee Guy: HERE: Coffee/large/milk/

Okay, not a very friendly exchange but there's a point! Let's look at what an
HTTP request looks like. 

Your web browser: GET http://facebook.com HTTP/1.1\n\n
The web server:   Returns the web page

So, let's break that down:

GET - this says what it sounds like, GET the page!
http://facebook.com -  the address
HTTP/1.1\n\n - this is the ony scary-ish part. HTTP/1.1 is the "version" of the
HTTP language we are speaking and teh '\n\n' are what are called newline characters
which signal that the request we are making is finished.

Don't believe me. Fine. Let's just try it. We're going to talk to a web
server in it's "native language" using a program called Telnet. Telnet is kind
of a raw way of communicating over a network using sockets/TCP (more on sockets
later and/or watch the lectures from Week 6 on TCP)

Telnet on Mac OS X:
http://www.wikihow.com/Use-Telnet-on-Mac-OS-X

Telnet on Windows:
https://kb.ctera.com/article/how-to-open-a-telnet-session-on-windows-7-or-windows-8-os-16.html

Your web browser:
GET http://students.purchase.edu/walter.meyer/resource/img/centralservices.jpg HTTP/1.1\n\n

### What is a socket?

A socket is a software abstraction that allows you to connect two pieces of 
software over a a network. These two pieces of software are usually
running on different computers. 

For example, your web browser uses a socket to connect to another web servers.

When you connect to a website your browser "creates" a socket and "connects" to
the web server in question. The web server also has a socket already "listening"
for connections. When it "hears" you connecting, it makes a connection back to
you and then you can both begin exchanging data with one another over this
connection.

When I say "abstraction" I mean that "under the hood" there is more
going on than would appear on the surface. 

In the same way that the gas pedal on a car is an abstraction that makes our car
"go faster" when we press it. That is, we press the gas pedal and 

A socket is really a software abstraction and "under the hood" TCP is being
used to transmit data between you and your destination.

### How does a socket work?

### Requirements

You are going to write two programs. 
In part I, you will write a client program.

In part II, you will modify your client program slightly and write a server
program. You will then be able to use these two to communicate with one another
using the console.

### Language

The assignment should be done using Python.

### Running your program

You should run your two programs like so:

```
python client.py www.purchase.edu > 



```

### Resources

https://docs.python.org/3/howto/sockets.html
https://docs.python.org/2/howto/sockets.html



```
 
```
