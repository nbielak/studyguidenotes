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

