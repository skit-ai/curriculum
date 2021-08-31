# HTTP

Hypertext Transfer Protocol (HTTP) is an application-layer protocol for 
transmitting hypermedia documents, such as HTML. It was designed for 
communication between web browsers and web servers, but it can also be used 
for other purposes. HTTP follows a classical client-server model, with a 
client opening a connection to make a request, then waiting until it receives 
a response. HTTP is a stateless protocol, meaning that the server does not 
keep any data (state) between two requests. Though this is not entirely true 
since you can make it stateful with use of cookies and sessions.

HTTP is a huge-impact, ever-evolving protocol with an equally long history. 
Here are the components that should help you start employing it:

## Overview

One of the most in-depth and the go-to documentation repository is [MDN Web 
Docs](https://developer.mozilla.org/). It is a great learning resource for web 
developers used by Mozilla, Microsoft, Google, Samsung[[1]](#1) and everywhere
. MDN has a great tutorial for getting the basics of HTTP right, [Overview of 
HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview). It will 
walk you through the basics and help udnerstand what different aspects are 
involved.

## HTTP Methods

HTTP defines a set of request methods to indicate the desired action to be 
performed for a given resource. Although they can also be nouns, these request 
methods are sometimes referred to as HTTP verbs. The most commonly used ones 
are GET, PUT, POST and DELETE. Together, these four methods make up the _CRUD_
, i.e., Create-Read-Update-Delete, interface for a resource.

Read about these and other methods [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) along with their specifications and browser support.

## Messages

You need to pass information between clients and servers. This is done through 
HTTP messages. There are two types of messages:

1. Request: Sent by the client
2. Response: Sent by the server

HTTP messages are text-based and consists of:

- Start Line/Status Line: The start line of responses are more appropriately 
called a status line. The start line for requests and responses consist 
differing information.
- Headers: HTTP header fields are a list of linefeed-separated HTTP data being 
sent and received by both the client program and server on every HTTP request. 
These headers are usually invisible to the end-user and are only visible to 
the backend programs and people maintaining the internet system.
- Body: The body of a message is usually where the major chunk of the message 
resides when large information is to be passed. This is where the contents of 
the associated resource resides.

Read about the HTTP messages [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages).

## Status Codes

HTTP response status codes indicate whether a specific HTTP request has been 
successfully completed. Responses are grouped in five classes:

1. Informational responses (100–199)
2. Successful responses (200–299)
3. Redirects (300–399)
4. Client errors (400–499)
5. Server errors (500–599)

You can find the status codes defined by section 10 of RFC 2616 on [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

# HTTP with REST

HTTP and REST are used interchangeably often. The reason is obvious, it's
almost everytime a convention that when you use HTTP, you practice REST. It's
true that HTTP and REST are two very different things.

REST stands for Representational State Transfer. It was first described in [Roy
Fielding’s now-famous dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm). REST is not a standard or a specification. Instead, 
Fielding described REST as an architectural style for distributed hypermedia 
systems. He believed there are several attributes of a RESTful architecture 
that would make it ideal for large interconnected systems such as the internet.

HTTP stands for HyperText Transfer Protocol, which is a standard with
well-defined constraints. It's a protocol maintained by the Internet Engineering
Task Force. While it is not the same as REST, it exhibits many features of a 
RESTful system. This is not by accident, as Roy Fielding was one of the 
original authors ofRFC for HTTP.

It’s important to remember that the use of HTTP is not required for a RESTful 
system. We do **insist** on it though. It just so happens that HTTP is a good 
starting because it exhibits many RESTful qualities.

## References

<a id="1">[1]</a>
[Wikipedia: MDN Web Docs](https://en.wikipedia.org/wiki/MDN_Web_Docs)
