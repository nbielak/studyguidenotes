# REST

Representational State Transfer
    making network communication more flexible and scalable

generic set of principles, not protocol

## The Fielding Constraints

### Client Server

network made up of clients and servers
    server = computer having resources of interest
    client = computer wanting to interact with those resources

sometimes act as server, other times as client

### Stateless

do not keep track of other's state

when client not interacting with server, server doesn't know of c's existence

each request standalone

### Uniform Interface

ensures that there is common language between servers and clients
    allows each part to be swapped or modded w/o breaking system


achieved through:
    identification of resources
    manipulation of resources through representations
    self-descriptive messages
    hypermedia

#### Constraint 1: Identification of Resources

affects identification of resources

resource could be anything
    HTML doc
    image
    info
    etc.

each identified by a stable identifier
    does not change across interactions
    does not change when state of resource changes

if resource moved to another identifier, server gives client bad request response and show link to new location

internet uses URI to identify resources and HTTP as communication

Client makes HTTP GET request to URI

#### Constraint 2: Manipulation of Resources

client manipulates resources through sending representations to server
    usually JSON

server has full control of resources
    responsible for any changes

    when client wants to make changes: sends server another rep.

#### Constraint 3: Self-Descriptive Messages

contains all info that recipient needs to understand it
    no additional info in separate doc or other message

req:
'''
GET / HTTP/1.1
Host: www.example.com

'''

    self-descriptive: told server what HTTP method and protocol

res:
```
HTTP/1.1 200 OK
Content-Type: text/html

<!DOCTYPE html>
<html>
  <head>
    <title>Home Page</title>
  </head>
  </body>
    <div>Hello World!</div>
    <a href= “http://www.recurse.com”> Check out the Recurse Center! </a>
    <img src="awesome-pic.jpg">
  </body>
</html>
```
    told client how it needs to interpret body of message

#### Constraint 4: Hypermedia

data send form servet to client
    contains info about what the client can do next

    i.e. any furter requests

in REST, servers only send hypermedia to clients

this whole system allows for clients to intelligently adapt to changes

underlying, server-side, implementation changes won't break clients

    bc each action self contained

    identifiers don't change with state

    hypermedia gives clients instructions

server does not need to remember anything about the client

## Other Fielding Constraints

### Caching

server responses should be labelled as cacheable or non-cacheable

caching occurs when client stores previous responses from server
    saves trip over network by using cached data

made possible by self-descriptive messages
    client knows all relevant data about single resource

### Layered System

can be more components than just servers and clients

each component constrained to only see and interact with next layer

proxy relays HTTP reqs to servers and other proxies
    additional component

    can be useful for load balancing and security checks

    acts like server to the intial client- sends req

    acts like client to relay that request

gateway translates HTTP req to another protocol
    propagates taht req
    
    translates res back to HTTP

client can treat gateway like server

### Code on Demand

only optional constraint

ability for a server to send executable code to client

HTML script tag
    HTML doc loaded -> browser automatically fetches JavaScript from server and executes locally


# Opening Google

## DNS Record Check

The browser checks the cache for a DNS record to find the corresponding IP address of maps.google.com.

DNS is a database that maintains name of website(URL) and linked IP address
    every URL has unique IP address

    IP address belongs to computer which hosts the server of the website

DNS: friendly to humans
    don't have to remember long numbers

checks 4 caches:
    1. browser cache
        repository of DNS records of previously visited websites for a fixed duration

    2. OS cache
        makes system call to underlying computer OS

        OS maintains cache of DNS records

    3. router cache
        with its own router that maintains cache

    4. ISP cache
        maintains its own DNS server

## DNS query

If the requested URL is not in the cache, ISP’s DNS server initiates a DNS query to find the IP address of the server that hosts website

purpose is to search multiple DNS servers on internet until if finds correct IP address

recursive search
    continues from DNS server to next 

    until IP found or error response

the ISP’s DNS server a DNS recursor whose responsibility is to find the proper IP address of the intended domain name by asking other DNS servers on the internet for an answer.

other DNS servers are called name servers
    perform DNS search based on domain architecture of website

domain levels:
    root domain: "."

    top-level domains: "edu", "gov", "org", "com", "au"

    Second-level domains: "'openoffice'.org", "'expedia'.gov", "'microsoft'.com

    Third-level domains: "'www'.expedia.gov",
    "'download'.microsoft.com"

requests send you through until found

data sent in small packets
    contain content of req
    IP address destined for

## TCP Connection

Browser initiates a TCP connection with the server

once browser receives correct IP address
    build connection with IP address server

    transfer information

user internet protocols to build connections
    TCP most common for HTTP requests

established using a process called TCP/IP three-way handshake
    client and server exchange SYN(synchronize) and ACK(acknowledge) messages to establish connection

    1. client sends SYN packet to server asking if open for new connections

    2. if server has open ports and can accept, sends ACK of the SYN package using an SYN/ACK packet

    3. client receives SYN/ACK packet and sends ACK packet

## HTTP Request

browser then sends HTTP req to the web server

contain 'GET' or 'POST', etc
    also browser identification

    types of reqs it will accept

    connection headers to keep TCP connection alive for additional reqs

## Server Response

sends HTTP response

contains webpage you requested from and status code(Content-Encodeing)
    how to cache the page(Cache-Control)

    cookies

    privacy info, etc

status codes:
    1xx: informational message
    2xx: success of some kind
    3xx: redirects the client to another url
    4xx: error on client's part
    5xx: error on server's part

## HTML Content

browser displays html content

renders barebone HTML skeleton

checks HTML tags and sends GET reqs for additional elements on page
    images
    
    CSS stylesheets

    JS fils

    these static files cached in browser