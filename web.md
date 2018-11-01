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

# DNS

backbone of the internet

user asks browser to visit website

What lifecycle methods get called in the mounting phase? What are the use cases for each of those methods?

## Who Makes It Work?

IANA- Internet Assigned Numbers and Authority
    maps domain names and IP addresses

    have mandate to make safe and stable DNS

ICANN- Internet Corporation for Assigned Names and Numbers
    technical operations of vital DNS resources

    defines policies for how the names and numbers of internet run

    "bottom up, consensus-driven, multi-stakholder model"

in 2015 ICANN transitioned from being under contract from US Department of Commerce to autonomous control of ICANN
    has board of directors 

    divided into separate member groups

ICANN treates public sector, private sector, and technical experts as peers

"In the ICANN community, you’ll find registries, registrars, Internet Service Providers (ISPs), intellectual property advocates, commercial and business interests,
 non-commercial and non-profit interests, representation from more than 100 governments, and a global array of individual Internet users"

    All points of view receive consideration on their own merit
        not equally

        more financial stake, more say

        AT&T, Verizon, Comcast, etc.

        could package websites like cable 
    Some gov'ts try to influence toward state interests

    IP advocates want more focus on IP and brand security
        usually lawyers protecting rights of high paying clients

    Commercial Service Providers (Google, FB) advocate users' privacy and web domination

    registries have interest in designing policy favorable to these groups

    Rregistrars will push back on ICANN sometimes

## End Users

lack of end-user engagement
    3.7 billion internet users, but few people own stakes

At-Large is end user contingent of ICANN
    divided by continent

# Packet, Routers, and Reliability

not direct dedicated connects

packet of information
    moves like one world a car

large packets broken down into smaller packets

router chooses how packet moves
    best route isn't always the best

    options make it fault tolerant
        if something breaks down can still work
    
TCP manages sending and receiving data as packets

scalable
    more routers, more reliable

## TCP Layers

### Application Layer

top layer
programs directly interact with
    http

### Transport Layer

TCP and UDP live here

after data gotten,
    talks to transport layer through port

breaks up data into packets

has header to double check everything goes through right

### Internet Layer

attach origin and destination IP address to packet

data then sent

# UDP and TCP

structure of packet: 

    Application, transportation, network, Link, Physical

UDP and TCP part of transport layer
    multiple apps uses one network connection simultaneously

    creates 1000s of ports per connection

message wrapped in segment in transportation layer
    has source and destination ports

segment passed to network layer

## UDP

small packet sizes

    udp headers 8 bytes, tcp 20 bytes

connectionless

more control over when data sent

primitive error deduction
    no error recovery
    corrupted segment discarded

UDP does not compensate for lost packets

packets may arrive out of order

no congestion control

lightweight but unreliable

## TCP

more reliable, bigger overhead

connection based
    negotiate connection first
    three way handshake
        SYN
        ACK
        SYN/ACK

retransmission
    when delivery ack not received assumes packet got lost and send again

implement in order delivery due to number system

congestion control
    delay transmission when network congested

Error detection
    checksum mandatory
    
Need bigger headers

Data doesn't always get sent out immediately
    side of congestion control

bigger overhead
    retransmission and package acknowledgement

UDP is message orient4ed
    sends data in distinct chunks

TCP stream oriented
    continuous flow of data
    split up in chuncks by TCP

# HTTP Methods

## GET

retrieves data from web server
    specifies params in URL

main method for doc retrieval

## HEAD

functionally similar to GET
    except res == line and headers, but no entity body

## POST

sending new data to server
    file update, form data

## PUT

req to store the included entity-body at a location specified by the given URL

## DELETE

delete file 
    location specified by URL

## CONNECT

by client to establish network connection to web server over HTTP

## OPTIONS

find out HTTP methods and other options supported by a web server

client can specify a URL for the OPTIONS method
    or an asterisk for entire server

## TRACE

echo the contents of an HTTP req back to the requester
    used for debugging purposes at the time of development

## HTTP Status Codes

### 200 OK

req has succeeded

res depends = 

GET: entity corresponding to requested resource in the response

HEAD: entity-header fields corresponding to the requested resource in response w/o message body

POST: entity describing or containing the result of the action

TRACE: an entity containing the req message as receive by the end server

### 201 Created

req has been fulfilled and resulted in a new resource being created

new resource can be referenced by URIs returned in the entity of response
    most specfic URI in Location header field

res should include an entity containing list of resource characteristics
    also locations from which the user can choose the one most appropriate

format specified by media type give in the content-type header field

origin server must create the resource before returning 201

if not carried out immediately,
    server should respond w 202(accepted)

### 204 No Content

server fulfilled req but does not need to return an entity boidy
    might want to return updated metaingormation

may include new or updated metainformation in the form of entity-headers
    associated with the req variant

if client is user agent
    should not change document view from that which caused the req to be sent

    response primarily intended to allow inputs  for actions to take place
        w/o causing change to the user agent's document view

        new or updated metainformation should be applied to the document currently in the user agent's active view

must not include a message-body
    thus terminated by the first empty line after the header fields

### 304 Not Modified

if client performed conditional get req and access allowed
    if doc not been modified
        responds with 304
    
must not contain a message body
    terminated by first empty line after the header fields

must include
    date unless its omission is required

if 304 indicates an entity not currently cached
    cache must disregard the response and repeat the req

if cache uses a recevied 304 res to update a cache entry
    cache must update the entry w new values

### 400 Bad Request

req cannot be fulfilled due to bad syntax

general error when fulfilling req would cause an invalid state
    domain validation errors, missing data, etc

### 401 Unauthorized

req requires user authentication

similar to 403 forbidden
    specifically for use when authentication is possible but has failed or not yet been provided

res must include a WWW-Authenticate header field containing a challenge applicable to the requested source

for missing or invalid auth token

### 403 Forbidden

for user not authorized to perform the operation
    or the resource is unavailable

legal req, but server is refusing to respond

authentication will make no difference

### 404 Not Found

used whe nthe requested resource is not found
    doesn't exist
    401 or 403 service wants to mask for security reasons

may be available in the future

subsequent reqs by the client are permissible

### 409 Conflict

whenever a resource conflict would be caused by fulfilling the req

duplicate entries and deleting root objects when cascade-delete is not supported are a couple of examples

### 500 Internal Server Error

generic error message given when no more qpecific message is suitable

general catch all when the server-side throws an exception

## HTTPS

HTTP vulnerable to changes by 3rd parties

secret messages sent by symmetric key cryptography

### Deciding the Key

SKC is secure if no one apart from sender and receiveer know the key

Man in the Middle Attack    
    3rd party gets key and changes message

    only protection is to change encryption system altogether

### Assymetrid Key cryptography

EXAMPLE:
    Bob sends a pigeon to Alice w/o message

    Alices sends pigeon back carrying a box with an open lock, no key

    Bob puts the message in the box, closes and locks the box, and sends the box to Alice

    Alice receives box and opens it with the key and reads the message

No third party can't change message bc doesn't have key

same process followed vice versa

even if you can encrypt message, can't decrypt

box is public key and the key is the private key

#### Certification Authority

3rd party to check to make sure everyone is truthfully the people they claim to be 

Use asymmetric cryptography to choose the encryption key for symmetric cryptography

reliablility of asymmetric cryptography and efficiency of symmetric cryptography

## GET vs POST

### Back button/Reload

GET: harmless

POST: data will be re-submitted

### Bookmarked

GET: can be bookmarked

POST: cannot be bookmarked

### Cached

GET: can be cached

POST: not cached

### Encoding type

GET: applicatoin/x-www-form-urlencoded

POST: applicatoin/x-www-form-urlencoded or multipart/form-data; use multipart encoding for binary data

### History

GET: parameters remain in browser history

POST: parameters are not saved in browser history

### Restriction on data length

GET: Yes, when sending dat, the GET method adds the data to the URL and the lenghtof a URL is limited

POST: no

### Security

GET: less secure bc data sent as part of URL; never use get for passwords etc

POST: safer bc params are not stored in browser history or in web server logs

### Visibility

GET: Data is visible to everyone in the URL

POST: not displayed in the URL


## PUT vs PATCH

PUT replaces entire entity, while PATCH only updates the fields that were supplied

# Cookies vs. localStorage vs. sessionStorage

## localStorage and sessionStorage 

localStorage and sessionStorage are relavtively new APIs
    pretty much identical

    sessionStorage only available during browser session
        does survive page reloads

        not window or tab closing

ongoing data needs to be stored in localStorage

localStorage and sessionStorage data can easily be read or changed from with the client/browser
    don't rely for sensitive or security -related data

## Cookies

can be tampered with by user

if storing sensitive info, use sessionStorage

in not using SSL, cookie info can be intercepted in transit, especially on open wifi

have a degree of protection
    from Cross-Site Scipting(XSS)/Script injection

        set HTTP only flag

        modern browsers will prevent access to the cookies and values from JS

    v important with auth cookies

all cookies valid fo a page sent from brower to server for evety req to the same domain
    bc cookies used for auth

    includes original page req, Ajax reqs, images, stylesheets, scripts, fonts

bc they are on every req, shouldn't store a lot of info

browsers sometimes impose size limits

used to store tokens for auth, session, advertising tracking

## All Three

only allow for storage of strings

Session storage generally allows for storage of primitives or obnjects

## Client-side vs. Server-side

HTTP is stateless protocol
    apps have no way of identifying a user from previous visits

    session data usually relies on a cookie token to identify the user for repeat visits

data will usually have a sliding expiry time
    stored in-process
        will be lost if the web server crashes or is restarted
    externally in a state server or database
        necessary when using a web-farm
session data completely controlled by app
    best place for anything sensitive or secure in nature
disadvantage of server-side 

data is scalability
    server resources are required for each user for the duration of the session

    data needed client side must be sent with each req

session data must expire after given time to avoid all server resources being taken up by abandoned sessions

when using session data
    be aware of the possibility that data will ahve expired and been lost
        esp on pages with long forms
    
    also lost if user deletes cookies or switches browsers/devices

can use hidden HTML inputs to persist dat from one page of a form to another to avoid session expiration

all are subject to same origin rules
    browsers should prevent access to the data except the domanin that set the information to start with

# XSS Attack

Cross-site Scripting Attack

client-side code injection
    attacket can execute malicious scripts
        malicious payload
    into legit website or web app

most rampant of web app vulnerabilites
    occurs when a web app makes use of unvalidated or unencoded user input within the output it generates

attacker does not target victim directly
    would exploit vulnerability within a website or web app that victim would visit

    using the website as a vehicle to deliver the malicious script to the victim's browser

can be taken advantage of in:
    VBScript
    ActiveX
    Flash

most widely abused is JavaScript

## How It Works

attacker must first find a ay to inject a payload into a webpage that the victim visits

could convince user to visit a vulnerable page with an inject JS payload

website needs to directly include user input in its pages

attacker can insert string that will be used within the web page and treated as code by the browser

## Effects

may not immediately stand out
    browsers run JS in a very tightly controlled environment

    JS limited access to the user's opeating system and files

has access to all the same objects as website
    cookies, which store session tokens

    can then impersonate user

JS can read and make arbitrary mods to the browser's DOM

can use XMLHttpRequest to send HTTP reqs with arbitrary content to arbitrary destinations

JS in modern browsers can leverage HTML5 APIs
    access geolocation, webcam, mic,specific fils from the user's file system

above with social engineering allow attaeckers to pull off advanced attacks
    cookie theft
    keylogging
    phishing
    identity theft

## Anatomy of XSS attack

needs 3 actors:
    website
    victim
    attacker

attacker injects payload in the websites database by submitting a vulnerable form with some malicious JS

Victim reqs the web page from the website

website servers the victim's browser the page with the attackers payload as part of the HTML body

victim's broswers will execute the malicious script inside the HTML body

## XSS Attack Vectors

### <script> Tag

most straight forward

can either reference external JS code or embed the code within the sceript tag

### <body> Tag

using the onload attribute or other more obscure attributes such as the background attribute

### <img> Tag

some browsers will execute JS found in <img> tag

### <iframe> Tag

allows the embedding of another HTML page int othe parent page

iframe can contain JS
    the JS in the iframe does not have access tothe DOM of the parent page

    due to the browser's Content Security Policy

still effective for phishing

### <input>

if type attribute set to image
    manipulated to embed a script

### <link>

link to external style sheets could contain a script

### <table>

background attribute of the table and td tags can be exploited to refer to a script instead of an image

### <div>

can spcify a background and thus, embed a script

### <object>

embed script from external site

# CSRF

Cross Site Request Forgery

not taken as seriously as it should
    stealthy and powerful attack

have major limitations though
    only allows for state changes to occur

    so cannot cater attacks that require the attacker to receive the contents of the HTTP response

malicious entity tricks victim into performing actions on behalf of the attacker
    impact depends on level of permissions of victim

    admin vs low level user

    exploits that web app completely trusts user after verifaction

1st part
    trick the victim into clicking a link or loading up a page
        social engineering
2nd part
    send crafted req to the victim's browser

    sent with values that attacker wants

    cookies, etc

    any request made with victim's creds will be legit

when req is made to web app
    browser check if it has any cookies for app

    auth data will be included in req sent to web app

    provides seamless experience, no reauthentication for every page

attacker may use CSRF to send reqs as if the victim is sending them
    w/o website being able to distinguish

## Understanding how an attack is carried out

only effective if user is authenticated
    victim must be logged in

bc CSRF used to bypass auth process
    some elements are not affected by CSRF

GET requests idempotent
    should not be used to perform state changes

## Preventing CSRF Vulnerabilities

### Ant-CSRF Tokens

most popular

token associated with user and can be found as a hidden value in every state changing form 

web server generates token

token is stattically set as a hidden input on the protected form

form is submitted by the user

token i included in the  post data

web app compares the token generated with the token sent in through the req
    match: req is valid, senf through form in web app

    no match: req considered illegal and rejected

tokens invalidated after some time

attacker would need to guess token

token needs to be cryptographically secure

### Same-Site Cookies

CSRF attacks only possible since cookies are sent with any req sent to a particular origin
    related to that cookie

flag can be set against a cookie, turning it into a same-site cookie
    can only be sent if req is being made from same origin that is related to the cookie being sent

    port and host are the same for both

not all browsers support them

# AJAX

AJAX = Asynchronous JavaScript And XML
    built in XMLHttpRequest obj
    JavaScript and HTML DOM

    might use XML to transport data
        equally common to transport data as plain text or JSON text

allows web pages to be updated asynchronously by exchanging data with a web server behind the scenes
    update parts of web page w/o reloading whole page

## XMLHttpRequest Object

supported on all browsers

`let xhr = new XMLHttpRequest();`

no access across domains
    both web page and XML file it loads must be located on the same server

A callback function is a function passed as a parameter to another function.

# Same Origin Policy

## Definition of an Origin

two pages have same origin if protocol, port, and host are the same for both pages

    "scheme/host/post tuple"
        where tuple is a set of three components that together compromise a whole

### Inherited Origins

scripts executed from pages with `about:black` or `javascript:` URL inherit the origin of the doc that opened the URL
    bc these types of URL od not contain info about the server of origin

    about:blank used as URL of a new empty popup window

Internet explorer exceptions
    trust zones
        if both domains are in highly trusted zone, then same origin limitations are not applied
            corporate domains

    Port: IE doesn't port into Same Origin components

## Changing Origin

a page may chage its own origin

script can set the value of document.domain to its current domain
    or superdomain of current domain

if superdomain, shorter domain is used for subsequent origin checks

port number kept separately by the browser

any call to setter causes port number to be overwritten to null

## Cross-Origin Network Access

same origin policty controls interactions between two diferent origins
    XMLHttpRequest or <img> els

3 categories:
    * cross origin writes typically allowed
        links, redirects, forms

    * cross origin embedding allowed

    * cross-origin reads typically not allowed
        read access leaked by embedding

        read width and heigh of an embedded image, actions of embedded script, or availability of embedded resource

### How to Allow Access

use cors to allow cross origin access

part of HTTP that lets servers share with clients information about what hosts are permitted to load within content loaded from that server

### How to Block Cross Origin Access

CSRF token
    cross-site request forgery


ensure that resource is not embeddable

ensure taht your resource cannot be interpreted as one of the embeddable formats listed above
    browser does not respect content-type

## Cross-Origin Script API Access

JavaScript APIs allow docs to directly reference each other

when two docs don't have the same origin
    refs provide very limited access to window and location objects

## Cross-Origin Data Storage Access

access to data stored in localStorage are separated by origin

Each origin gerts its own separate storage
    JS in one origin cannot read from or write to the storage belonging to another

Cookies use a separate definition of origins
    page can set a cookie for its own domain or any parent domain
        as long as the parent domain is not a public suffix

# Cross-Origin Resource Sharing

CORS

mechanism that uses additional HTTP headers to tell browser to let web app running at one origin access selected resources from server at different origin

    cross-origin HTTP req

browsers restrict cross-origin HTTP reqs initiated within scripts

supports secure cross-orign reqs and data transfers between browsers and servers

modern browsers use CORS in an API container to mitigate rists of cross origin HTTP reqs
    XMLHttpRequest

    Fetch

## What Requests Use CORS?

used to enable
    XMLHttpRequest or Fetch APIs in a cross-site manner

    Web Fonts
        cross-domain font usage in @font-face

        so servers can deply TrueType fonts taht only be cross-site loaded and used by permitted sites

    WebGL textures

    Images/video frames drawn to a canvas using drawImage()

## Functional Overview

works by adding new HTTP headers 
    allow servers to descibe the set of origins permitted to read taht info using a browser

HTTP req methods that can cause server data side-effects
    browsers "preflight" the req
        soliciting supported methods from the server with HTTP OPTIONS req method

        upon approval, send the req with the actual HTTP req method

Servers also notify clients whether credentials must be sent with reqs
    cookies, HTTP Auth data

CORS failures result in errors
    for security, specifics not available to JS code

    look at browser console for details

some reqs don't trigger a CORS preflight
    simple requests

    only allowed methods
        GET
        HEAD
        POST

    besides headers set automatically by the user agent, only headers which are allowed to be manually:
        those which Fetch spec defines as being a "CORS-safelisted request-header"

    only allowed values for the Content-Type headers are:
        application/x-www-form-urlencoded

        multipart/form-data

        text/plain

    No event listeners are registered on any XMLHttpRequestUpload obj used in req
        accessed using the XMLHTtpRequest.upload property

    No ReadableStream object is used in the req

no res data is released to requester unless server sends appropriate header
    sites that prevent CSRF have nothing new to fear from HTTP access protocol

## HTTP Response Headers

headers that servers send back for access control requests

### Access-Control-Allow-Origin
    
for returned resource

    `Access-Control-Allow-Origin: <origin> | *`

specifies either a single origin
    tells browsers to allow that origin to access a resource

the "*" wildcard
    reqs w/o credentials

    to allow any origin to access the resource

### Access-Control-Expose-Headers

lets server whitelist headers that browsers areallowed to access

```js
Access-Control-Expose-Headers: X-My-Custom-Header, X-Another-Custom-Header
```

allows headers to be exposed the browser

### Access-Control-Max-Age

how long the results of a preflight req can be cached

```js
Access-Control-Max-Age: <delta-seconds>
```

### Access-Control-Allow-Credentials

whether or not the res to the req can be exposed when credentials flag is true

when used in res of preflight req
    should actual req be made using credentials

```js
Access-Control-Allow-Credentials: true
```

### Access-Control-Allow-Methods

specifies methods allowed when accessing the resource
    used in res to preflight req

```js
Access-Control-Allow-Methods: <method>[, <method>]*
```

### Access-Control-Allow-Headers

res to preflight req
    which HTTP headers can be used when making the req

```js
Access-Control-Allow-Headers: <field-name>[, <field-name>]*
```

## HTTP Request Headers

headers that clients may use when issuing hTTP reqs
    to make use of cross-origin sharing feature

set when making invocations to servers

developers using cross-site XMLHttpRequest capability do not need to set any x-origin sharing req headers programmatically

### Origin

the origin of the cross-site access req or preflight req

```js
Origin: <origin>
```

URI indicating the requesting server

no path info, just name

can be empty string
    useful for if source is a data URL

origin header is always sent

### Access-Control-Request-Method

used when issuing a preflight req to let server know what HTTP method will be used for req

```js
Access-Control-Request-Method: <method>
```

### Access-Control-Request-Headers

issuing preflight req to let server know what HTTP headers will be used for actual req

```js
Access-Control-Request-Headers: <field-name>[, <field-name>]*
```

# SQL vs. NOSQL

MongoDB - NoSQL
    not SQL calls against tradition tables and rows

## Genesis of NoSQL

used to have structured data
    numbers, dates, etc

    displayed in titled columns and rows

    run queries in SQL

wanted intelligence from data
    how were sales, regions, etc

data divided into operational and analytical
    data warehouses

more data, less like SQL

SQL relational servers are built to handle demand of financial transactions

designed around tenets of ACID
    Atomicity
    Consistency
    Isolation
    Durability

ensure only one chage can be written to a data field at a time
    no conflicting transactions

    no matter which server you ask, get the same value

ACID doesn't matter much for data analysis
    database locks of SQL can get in the way

interntet resulted in "web-scal attacks"
    hunderd -> millions of people wanting access to same data sources at the same time

to scale you could buy a bigger server
    expensive

    companies turned to distributing database out over hundreds or thousands of servers

NoSQL database associated with big data tasks, handling large volumes of data in various forms
    columnar dbs, for dealing with massive collections of simple structured data
    
    Key-value and other unstructured dbs
        MongoDB

        use rules defined by programmers to comb through large amounts of unstructured data, includeing docs and websites

    High-speed databases for processing large streams of data with low latency
        those diverging tasks have driven the evolution of dif tech taht get lumped together as NoSQL

        provide some of the relational quality tuned to handle demands of big data

## Hadoop

not really considered db

designed as cheap way to store data and process it

enabled by Google's MapReduce
    process and generate large data sets with a parallel, distributed algorithm on a cluster

Hadoop not user-friendly
    needs trained, talented experts

needs db handlers and front end

land data, find data scientists to find relationships, turn that into requirements that yield a system

## MongoDB

most popular NoSQL database

designed from onset to make degs maximally productive

major cost isn't servers or hardware
    it's developer's speed

## Couchbase

cluster of unreliable commodity hardware

open sourece, NoSQL distributed JSON-based document store

CP type system
    gives consistency and partition tolerance

CAP 
    consistency
    availability
    partitionability

    distributed computer system can only gurantee 2/3

outgrowth of CouchDB
    opensource database

performace in terms of user scale

elasticity
    ability to grow, shrink, cluster while under load without downtime

Cross Datacentert Replication
    XDCR
    ability to replicate data from one cluster to another
        primarily for disaster recovery

not so agile

## VoltDB

NewSQL
    reworking of relational database management systems
    
    promised extreme scalability for online transaction processing (OLTP)
        like NoSQL
    
    same guarantees of ACID

VoltDB is one example
    distributed, in-memory, parallel NewSQL relational db

dat's more useful when fresh

## Convergence

most use both SQL and NoSQL
    integrating

## More on SQL vs. NoSQL

relational vs. non-relational
    how they're built
    type of info
    how they store

relational dbs structured
    like phone book with name, number, address

non-relational dbs document oriented and distributed
    file folders that hold everythign from a person's address and phone number to their FB likes 

### SQL: Relational DBs

more rigid, structured

two or more tables with cols and rows
    each row an entry

    each col sorts a very specific type of info

relationship called schema
    schema must be defined before anything added

stored data msut be structured well
    a well designed schema minimizes data redundancy

    prevents tables from becoming out-of-sync
        critical to business recording financial transactions

Structure Query Language
    programming language used by database architects to design relational databases

    exectutes queries, retrieves data, edits data, deletes, creates new records

    lightwieght, declarative

    like a server-side-script

    JOIN clause powerful
        developers can retreive data stored across multiple tables

    fits well into many software stacks
        LAMP, Ruby-based stacks

### NoSQL DBs

flexible

document oriented
    non structured data stored in a single document that can be easily found but isnt' necessarily categorized into fields

    storing data in bulk requires extra processing effort

eases of access
    sidestep relational issues with APIs that allow devs to execute queries wihtout having to lear SQL

#### Common Types of NoSQL DBs

1. key-value model
    least complex

    stores data in a schema-less way that consists of indexed keys and values

2. Column store
    wide column store
    stores data tables as coluns rather than rows

    sectioning out columns allows for excellent scalability and high performance

3. Document database
    key-value concept with complexity

    each doc has its own data and unique key, used to retreive it

    great option for storing, retrieving, and managing data that's document oriented but still somewhat structured


### Reasons for SQL DB

need to ensure ACID compliance
    reduces anomalies and protects integrity of your db

    prescribes exactly how transactions interact with the db

    NoSQL tends to sacrifice ACID compliancy flr flexibility and processingspeed

data is structured and unchanging
    if not growing and don't need more servers

    consistent data

### Reasons for NoSQL

storing large volumes of data that have little to no structure
    sets no limits on the types of data you can store together

    add diffent new types as your needfs change

    can store data in one place w/o defining what types of data those are in advance

making the most of cloud computing and storage
    excellent for cost saving, but requires data to be easily spread across multiple servers to scale up

Rapid development
    data doesn't need to be prepped ahead of time

# Scalability

## Vertical Scaling

get more RAM, processing, disk space

exhaust financial resources or state of the art abilities

## Horizontal Scaling

a bunch of cheaper machines

load balancers distribute requests

Round Robin
    start with server one...n

    and wrap around

    one server could get overloaded

    caching can cause heavier load on servers

load balancing to not busy servers
    break session

    no redundancy, bad if anything breaks

### RAID

Redundant Array of Independent Discs

RAID0
    stripe data across them
        write to one then the other then the first...

    doubles speed of writing

RAID1
    mirror file

    store both places

    a little slower

RAID10
    combination of RAID0 and RAID1

RAID5
    3-5 drives, but one is redundant

RAID6
    any two drives can die, but data still stored

### Load Balancing


