## Programming Project: TCP Sockets

### [Introduction](#intro-anchor)

This is going to be a 2 part project.

Part I is just a gentle introduction into HTTP and TCP.

In part II, you will write your own web server.

### [Part I: Act like a browser, think like a hacker.](#part1-anchor)

When you use the web, you typically do so in a browser.
Underneath the graphical user interface of your browser, there are many protocols in use.

Namely, Ethernet, IP, TCP, and HTTP.

These protocols are part of the so-called layers of the Internet. You will learn about these protocols in more detail throughout the course.

For this project, we are going to focus on TCP and HTTP.

First, we will cover the basics of how HTTP works.

When you go to a web page in your browser what is happening behind the scenes?

How does the server you are visiting: Facebook, CNN, GitHub, etc. know what you want to see?

It "knows" because of the HTTP protocol. A protocol is just a way in which two or more things communicate. In the case of computers, these two things are typically software programs.

Generally speaking, this is the client/server architecture of the web. There is a client, who wants to get data and a server who sends data to the client. The client and the server must establish a "protocol" or set of rules for communicating with eachother.

The HTTP protocol is pretty simple. Protocols like HTTP are much like the protocols
those we use in our everyday life. For example, this morning I bought
my coffee from dingy looking cart few blocks from my apartment:

* **ME**: I want a large coffee with milk.
* **COFFEE GUY**: (Hands me a large coffee with milk.)

Okay, this is basically how HTTP works. I'm not kidding. Let's make my morning
coffee routine slightly more "computer like".

* **ME**: ```GET: Coffee/large/milk/```
* **COFFEE GUY**:  ```(Hands me a large coffee with milk.)```

Okay, not a very friendly exchange, but there's a point! Let's look at what an actual
HTTP request looks like.

Your web browser makes an HTTP request that looks like this:

**ME**:
```
GET /index.html HTTP/1.1\n\n
```
**WEB SERVER**:
```
(Returns the web page!)
```

Okay, let's break that down:

```GET``` - this says what it sounds like, GET the page!

```/index.html``` -  this is the file we are asking the web server for.

```HTTP/1.1\n\n``` - this is the only scary-ish part. ```HTTP/1.1``` is the "version" of the
HTTP language we are speaking and the ```\n\n``` are what are called newline characters
which signal that the request we are making is finished.

![Client Server Diagram](/img/clientserver.png)

Don't believe me? Fine, let's just try it. We're going to talk to a web
server in it's "native language" (HTTP) using a program called Telnet. Telnet is kind
of a "raw" way of communicating over a network using sockets and TCP (more on sockets
later--be sure to [watch the lectures from Week 6 on TCP](https://www.coursera.org/learn/internet-history#syllabus)).

#### Telnet Setup

Telnet on Mac OS X:
http://www.wikihow.com/Use-Telnet-on-Mac-OS-X

Telnet on Windows:
https://kb.ctera.com/article/how-to-open-a-telnet-session-on-windows-7-or-windows-8-os-16.html

Okay, once you have telnet setup on your computer, you should be able to open your Terminal app (Mac OS X) or cmd app (Windows) and type the following (*Note: the $ character is part of the shell 'prompt' you do not type it*):

```
$ telnet www.google.com 80
GET / HTTP/1.1
```
* Now, press RETURN twice (this us sending those ```\n\n``` characters)

* What do you see?

What about trying this:

```
$ telnet www.google.com 80
GET /maps HTTP/1.1
```

* What do you see now?

Try the same thing on a few other websites.

So, that is essentially how HTTP works. Admittedly, this is an oversimplification, but this is the essence of the protocol.

### Part II: BYOWS: (aka) **B**uild **Y**our **O**wn **W**eb **S**erver

What is a web server? Well, a web server in its simplest form is a program that serves web pages to web browsers! Okay, that isn't very clear, is it?

More specifically, when your browser visits a website it is asking the web server for a particular file. Much like we did in Part 1, the web server is responding to these so-called GET requests that are part of the HTTP protocol. So, when the web server sees your get request it tries to return the file requested in the GET request.

So, take this GET request for example:


```
$ telnet students.purchase.edu 80
GET /walter.meyer/index.html HTTP/1.0

```
* Now, press RETURN twice (this us sending those ```\n\n``` characters)

What file do you think we are asking for there?

What does the prefix of ```/walter.meyer/``` before the ```index.html``` mean?

We are asking for a file called ```index.html``` inside of a folder called ```walter.meyer```.

So, if the web server returns a file to you your browser proceeds to display it. Remember, a web page is just HTML contained in a file that your web browser "renders".

### How does a socket work?

A socket is a software abstraction that allows you to connect two pieces of
software over a network. These two pieces of software are usually
running on two different devices. e.g. your phone's web browser and a web server out on the Internet.

You can think of sockets like the two ends of a pipe. When you want to connect to a web server, your device begins a connection setup process that, if successful, results in the a virtual "pipe" being constructed between you and the server in question.

![Pipe Diagram](/img/pipe.png)

When you connect to a website your browser **creates** a socket and **connects** to
the web server in question.

The web server you are connecting also has a socket already **listening**
for connections. When it "hears" you connecting, it makes a connection back to
you and then you can both begin to communicate with one another over this
connection.

Wait, how does this fit in with HTTP? Well, in some sense the language of HTTP is being "spoken" through this virtual pipe. That is, two computers use TCP to setup a pipe for communication and then talk to each other through this pipe using another protocol. In the case of the web, HTTP!

So, a socket is really a software abstraction and "under the hood" TCP is being
used to transmit data between you and your destination. This allows for the reliable transfer of data over the Internet. Remember, you will learn that the the Internet, that is, the IP protocol, is inherently unreliable. That is, it can "drop" or "lose" packets. TCP is used to ensure that data can be delivered reliably between computers in spite of this.

### Building Your Own Web Server
You are going to write a web server that is able to "serve" files from your computer to web clients (your web browser of choice). This is essentially what a real web server does.

Your web program (server) should behave like this:

1. Start your server

```
python simple_server.py 3000

```
Where ```3000``` is the port you are running your server on.

2. Create a ```test```directory in the same location your simple_server.py program is stored.

3. Create an index.html file with some basic HTML in it. We will use this to test your server.

```
simple_server.py
\_test
  \_index.html
```

4. In your Web browser visit the following URL:

http://localhost:3000/test/index.html

If the page renders correctly, you have done it--your server works! Read on for how to get started on programming.

### Beginning Hints
You should use an "iterative" development style when writing code.

For example, don't try to implement everything at once. Rather, try to get your server to simply respond to GET requests without serving files. Before that, just make sure your program can do basic things. Use ```print``` statements to help you debug and test your code.

Once you have everything working, begin trying to send files to the browser.

You will need to import the following libraries, at a minimum, to get your code to work

```Python
import sys    # for getting arguments passed to your program when you run it
import socket # for sockets
```

### Getting Started with the Python Socket Library

Remember how a simple Python program starts out, right? Here is a refresher:

Your file should be named ```simple_server.py``` and contain the following at minimum:

```Python
if name == "__main__":
    print "Hello World!"
```

If you've programmed in Python before, this program will be, in many ways, similar to others you have written. You will need to use variables, accept arguments, manipulate strings, etc.

However, the major difference when writing a server is that you need to use sockets. Luckily, Python provides a great socket library that will make it easier for you to get started.

Remember, your program will be the server. As such, there are 5 steps to creating a socket that can handle client requests. See the code excerpts below.

```python
# 0. Import the socket library so we can actually use it!
import socket

# 1. Create a socket
my_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# 2. "Bind" the socket to an IP and PORT
my_socket.bind((host, port))

# 3. Begin "listening" on the socket
my_socket.listen(5)

# 4. Begin "accepting" client connections
conn, addr = my_socket.accept()

# 5. Receive some data (up to 1024 bytes) FROM the client
data = ''
conn.recv(1024)
print data

# 6. Send some data back TO the client
conn.sendall("Hello Web Client!")
```

Feel free you use this code to start out.

![Socket Diagram](/img/server.png)

Now, once you have your program to a point where you thing it is working and creating a socket, try connecting to it in your web browser or use telnet again.

If you started you server like so:

```
python simple_server.py 3000

```
Where ```3000``` is the port you are running your server on.

Then you would access your server in your browser at the following URL:

http://localhost:3000/

### Submissions

Submissions will be done using Git (GitHub Classroom).

You should familiarize yourself with how to use Git:

https://help.github.com/articles/good-resources-for-learning-git-and-github/

If you are working on a team, you will elect one member who will submit their GitHub repository.

### Additional Resources

Sockets:

https://docs.python.org/3/howto/sockets.html
https://docs.python.org/2/howto/sockets.html

HTTP:

https://www.tutorialspoint.com/http/http_parameters.htm
https://www.tutorialspoint.com/http/http_messages.htm

### Academic Integrity

It is imperative that you do not copy and paste code from the Internet, books, or elsewhere.

If you do, we will be able to tell. Don't do it.

This does not mean that you can't research the ways other people have tackled a particularly programming problem or look at other code. It means you cannot plagiarize code in the same way you wouldn't for an essay. If you are using a particular Internet resource, StackOverflow, etc., please cite it in your submission.

If you are at a point where the assignment feels completely overwhelming or you are at a loss as to what to do, talk to or email me. I will help you!

https://www.purchase.edu/Policies/academicintegrity.aspx

### Questions / Concerns

Email me or post to Moodle!
