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

