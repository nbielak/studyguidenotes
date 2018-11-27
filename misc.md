# Benefits of HTML5

## Accessibility

accessible sites easier: semantics and ARIA

    header, footer, nav, section, aside, etc

    screen readers easily access content

    no way to determine what given div was w/o id or class

ARIA W3C spec used to assign specific roles to elements in HTML doc
    important landmarks on page

## Video and Audio Support

video and audio tags
    had to use <embed> and <object>

    now <video src="url" width="" height="" autoplay/>

## Doctype

cleans up head tags 

## Cleaner Code

can use semantic and HTML headers to describe content

## Smarter Storage

local storage feature

cross between cookies and client side database

allows for cross storage across multiple windows

better security and performance

data persist after browser is closed

## Cross Browser Support

## Mobile
    viewport allows you to define widths and zoom settings

    full screen browsing

    homescreen icons

# Media Queries

`@media` rule include block of CSS only if condition === true

can add breakpoint where certain parts of design behave differnetly on each sider of the breakpoint

## Design for Mobile First

look for changes when screen size gets bigger than certain point

can add as many as you like
    mobile - tablet - desktop

good to make breakpoints for device size

can change layout of page depending on orientation of browser
    portrait vs. landscape

can also hide elements with media queries
    font size tooS

# CSS Grid

fundamental to design of websites

two core ingredients:
    wrapper(parent)
    items(children)

give display of 'grid'

## Columns and Rows

make it two dimensional

use `grid-template-columns` and `grid-template-rows`

position and resize: `grid-column` and `grid-row`

# React 

## Fundamentals

### React is all about components

define small reusable components to put them together to build bigger ones

component name starts with capital letter
    required because of mix of HTML and React elements

    lowercase for HTML

every component has attributes
    list is called props

### JSX

document.createElement
    main function in the React top-level API

    like document.createElement

    higher-level function that can create React components

    accepts dynamic number of arguments after the second one to represent the children of the created element

        createElement actually creates a tree

React's API as similar to DOM API as possible

jsx provides ability to write syntax very similar to HTML
    not html
        doing className instead of class

### JS expressions in JSX

use {} for any JS expression

only expressions
    e.g. no if statement, but ternary expression is ok

JS variables are also expressions
    component receives props, props can be in curly braces

JS objects are also expressions
    one use case is to pass a CSS style object

use destructuring

React element is also an expression

### Can write React components with JS classes

`class xxxx extends React.Component`

### Events in React

all React element attributes are named using camelCase

pass JS function reference as the event handler rather than a string

### Every REact component has a story

class components only

1. define a template for React to create elements from the component

2. instruct React to use it 
    render call of another component

3. React instantiates an element and gives it a set of props
    this.props

4. JS constructor method called, if defined
    first of the component lifecycle methods

5. Computes the output of the render method

6. On first render, React communicates with browser using DOM API to display the element there
    known as mounting

7. invokes another lifecycle method
    componentDidMount
    do things on the DOMthat we now know exists in the browser

8. Sometimes ends here
    other components get unMounted from the browser DOM
        componentWillUnmount

9. The state of any mounted element might change
    the parent of that element might rerender

    mounted element might recei e a difference set of props

### React Components can have private State

only applicable to class components
    presentational components = "dumb"

React monitors every component state for changes
    have to change state field through `this.setState`

setState is asynchronous

merges what you pass it with existing state

### React will react

reacts to state changes
    not reactively but on a schedule

render function's input:
    props that e passed by the parent

    internal private state that can be updated anytime

### React is your agent

to communicate with browser

### Every React Component has a story pt 2

1. component might re-render when state updates
    or when parent decides to change the props it passed to the component

2. if latter, React invokes componentWillReceiveProps

3. for any change, React asks shouldCompnentUpdate
    can customize or optimize render process

    return true or false

4. default is fine though

5. invokes componentWillUpdate
    computes new rendered output and compares with last output

6. if rendered output is the same, React does nothing

7. React takes difference to browser, if there is one

8. invokes componentDidUpdate


## Lifecycle Methods

control what happens when each tiny section of UI renders, updates, rerenders, or disappears

### componentWillMount

component will appear on screen very shortly

don't want to do much
    bit of a dud

    no component to play with, so no DOM manipulation

    nothing has changed since component's constructor was called
        where default config set up

default position

do anything that needs to be done at runtime here
    connecting external APIs

    should be done in root component, though

### componentDidMount

load data here

"You can’t guarantee the AJAX request won’t resolve before the component mounts. If it did, that would mean that you’d be trying to setState on an unmounted component,
which not only won’t work, but React will yell at you for. Doing AJAX in componentDidMount will guarantee that there’s a component to update"

other things to do:
    draw on <canvas> element

    initialize masonry grid layout

    add event listeners

do setup you can't do w/o DOM

### componentWillReceiveProps

new data being sent down as props

have access to nextProps and current Props (this.props)

What to do:
    1. check which props change

    2. if props change significantly, act on it

not on initial render
    no old props to compare new props to

most commonly used to act on particular prop changes to trigger state transitions

can call setState

### shouldComponentUpdate

called with nextProps and nextState

always return a boolean
    answer to question "should I rerender"

good way to improve performance and not waste renders

no setState

### componentWillUpdate

functionally equivalent to componentWillReceiveProps

not allowed to call setState

most commonly used instead of componentWillReceiveProps when component has shouldComponentUpdate and no access to prev props

### componentDidUpdate

can do same stuff as componentDidMount

common use to update DOM in response to prop or state changes

can call setState

### componentWillUnmount

last minute requests

cancel outgoing network reqs, remove event listeners


# Redux

## The Single Immutable State Tree

whole state as a single javascript object

all changes explicit

more complex app == more state to keep track of

## State Changes with Actions

state tree read only

dispatch an action
    action is an object describing the change

    only req is that it has a type quality

describing in a minimal way what the data changed

any change gets there through actions

## Pure and Impure Functions

### Pure

return value depends solely on args

no discernable side effects
    database calls etc

same args, same return value

don't modify args

### Impure

may call database or network

may operate on DOM

may override values

may have side effects

some functions in Redux have to pure

## The Reducer Function

view layer most predictable when described as pure function

state mutations need to be described as pure function
    takes prev state and action
    returns next state

## Store Methods

holds state obj

dispatch actions

specify reducer to update state

getState
    returns current state

dispatch
    dispatch actions to change state

subscribe
    register callback any time action is dispatched

    can update UI to match current app state






# SQL Query Order

1. FROM and JOIN
    includes sub queries in this clause

    can cause temporary tables to be created under the hood

2. WHERE
    first pass constraints applied to the individual rows

    rows that do not satisfy are discarded

    only access columns directly requested in the FROM clause

    SELECT aliases not accessible

3. GROUP BY
    remains rows grouped based on common values in the GROUP BY clause

    only be as many rows asthere are unique values in that column

    only need to use this when you have aggregate functions

4. HAVING
    if GROUP BY, then constraints in HAVING are applied to the grouped rows

    aliases not accessible

5. SELECT
    select expressions computed

6. DISTINCT
    rows with duplicate values discarded

7. ORDER BY
    rows sorted by the specified data in ascending or descending order

    can ref aliases

8. LIMIT/OFFSET
    rows outside of these discarded
    
    leaving final set of rows

# SQL JOINS

inner, left, right, full

Inner Join
    where Venn Diagram meets

    returns records at the intersection of two tables
Left Join
    everything in left side and center

    all records from a and anything matching from b

    NULL if no info
Right Join
    everything in right side and center

    mirror to left
Full Join
    everything

# SQL Subqueries

inner or nexted queries

perform operations in multiple steps

easiest to start with the FROM

first inner query is run
    then outer query runs with the results of the inner query

# Networking

vary voltage to send information in cables

symbols
    5v = 1
    0v = 0

BOD
    symbols per second

ASCII to map numbers to text

Fiber Optics
    2 strands

    have glass cladding


Wireless
    fluctuate waves

clock rate very important
    transition rate

    clock slips if not synced up

    can be synced by GPS antennae
        by atomic clock in computer

        send seperate signal with clock
            might be slightly slower

            could get out of phase
    
        can combine clock and data
            0 -> 5 = 1
            5 -> 0 = 0

            manchester coding
            
            don't need perfectly synced clocks

## HDLC

High Level Data-Link Control

uses frame delimiter or flag
    01111110 - starts frame

    every 8 bits makes up byte

    put 0 after five consecutive 1s
        not to confuse with flags

        ignores 0

        bit stuffing

## Ethernet

uses silence to show no frame

then sends preamble

56 bits of alternating 1s and 0s
    gives opportunity for receiver to sync clock

start of frame delimiter ends in '11'
    receiver knows the next bit is first bit of data

then reads data

frame size varies from 64-1500 bytes

## Frame Formats

point to point links not common
    service providers usually

    one computer on each end of link

Multipoint/broadcast
    share data link and communicate with each other

    ethernet switch
        common way

### Ethernet format

    MAC address is unique address

    preamble/SFD

    Destination address
        unique
        6 byte
    Source Address
        6 byt

    Ether Type
        2 bytes

        payload type

    Payload
        46-150 bytes long
        
    last 4 bytes frame check sequence
        used to detect corrupted data

### PPP format

common in point to point

Flag and beginning and end

Address and Control
    each one byte long

Protocol
    same as ether type

Payload

Frame Check sequence

## IP Address

Internet Protocol address

send info between networks

building table of addresses is routing

using table to forward packets is forwarding

use 32 bit address
    use prefixes to send right direction

    takes longest matching prefix

ARP
    address resolution protocol

    sends message to network to check IP addresses 

## TCP

provides byte stream service

reliable
connection oriented
    host has to connect to other

either side can send stream of bytes

encapsulated in IP packet

# Website Enhancements

improving site speed improves performance

google takes speed into consideration when ranking sites

mobile first index now

3 second load time ideal

## Minimize HTTP requests

80% of load time is spent downloading parts of page
    images, stylesheets, scripts

## Minify and combine files

JS, CSS, and HTML files

minifying
    removing unnecessary formatting, whitespace, and code

combine all CSS and JS into one file

## Asynch loading for CSS and JS

when browser loads a page moves top to bottom

## Defer JS loading

prevent from loading until after other els

## Minimize Time to First Byte

TTFB
    amount of time a browser has to wait before getting first byte of data

    server side concern

influenced by internet connection

## Reduce Server Response Time

amount of time DNS lookup takes

switch to faster DNS provider

## Choose Right Hosting Option

upgrade when getting more traffic

Shared hosting 
    cheapest

    CPU, diskspace, RAM with other sites on same servrer

VPS hosting
    share server, but have own dedicated portions of the server

Dedicated hosting
    much more space, but more configuration and technical set up

    most expensive

## Run a Compression Audit

smaller files load faster

## Enable Compression

gzip
    file format and app that locates strings of similar code in files then temporarily replaces them to make the files smaller

works well with CSS and HTML

## Enable Browser Caching

can load info without having to send HTTP request

## Reduce Image Size

jpg
    lossy

png
    lossless

## Use a CDN

networks of servers to decrease load times

cache site on a global network of servers

## External Hosting Platforms

for larger files, like videos

host video on youtube and embed on site

## Optimize CSS Delivery

one external style sheet

## Prioritize Above-the-fold content

top of the page load faster

lazy loading

user doesn't need to wait to access page

## Reduce Number of Plugins

not heavy weight, but too many can slow down site

## Reduce Redirects

necessary when move or delete page or broken links

cna create additional HTTP reqs

## Reduce External Scripts

third party integrations

## Monitor Speed Over Time

## Moniter Mobile Page Speed

# DOM Tree

every HTML tag is an object

nested tags are called children of the enclosing one

text inside is obj as well

tags are called element nodes

text nodes contain only a string
    may not have children, only leaf

spaces and newlines are special characters
    form text nodes and become part of the DOM

spaces and newlonies before head are ignored

anything after closing body tag moved inside the body

## AutoCorrection

if browser encounters malformed HTML 
    corrects when making the DOM

tables must have `<tbody>`

## Other Node Types

if something is in HTML, it also must be in the DOM tree

document obj that represents the whole doc is a DOM node as well

12 types of node, but usually work with 4
    document: the entry point

    element nodes: HTML-tags, the tree building blocks

    text nodes: contain text

    comments: won't be shown, but JS can read it from the DOM

## DOM Traversal

start with document object
    from it we can access any node

### documentElement and body

topmost tree nodes are available as document properties
    `<html>` = `document.documentElement`

    `<body>` = `document.body`
        can be null

        null means doesn't exist

    `<head>` = `document.head`

### Children

child nodes or children
    elements that are direct children
        nested exactly in given one

descendants
    all elements that are nested in the given one including children and their children, etc.

childNodes collection provides access to all child nodes including text nodes

firstChild and lastChild give access to the first and last children

### DOM Collections

childNodes looks like an array, but is a collection
    special array-like iterable obj

can use `for..of` to iterate
    don't use for..in

    will go over all enumerable properties

Array methods won't work because not an array
    can use Array.from

DOM collections read only

DOM collections live

### Siblings and the parent

siblings
    nodes taht are children of the same parent

parent is available as `parentNode`

next sibling is `nextSibling`, same with previous


### Element-only Navigation

previous navigation properties reger to all nodes
    `childNodes` allows us to see both textnodes, el noses, and comment nodes

    many tasks we don't want text or comment nodes

    want to manipulate el nodes that represent tags and form the structure of the page

links are similar, but include `Element` inside
    `children`- only those children that are element nodes

    `firstElementChild`, `lastElementChild`

    `previousElementSibling`, `nextElementSibling`

    `parentElement`

## DOM Nodes

### DOM Node Classes

diff properties depending on their class
    `<a>` has link-related properties

    text nodes not el nodes

common properties and methods between all of them

EventTarget
    root of hierarchy
        root abstract class
    Objects that are classes are never created

    serves as a base
        so that all DOM nodes support 'events'

Node
    also an abstract class
        serves as base of DOM nodes

    core tree functionality
        parentNode
        siblingNode
        childNodes

    objects of Node class never created

    Text, Comment, and Element inherit from it

Element
    base class for DOM els

    provides element level navigation
        nextElementSibling
        children
        getElementsByTagName
        querySelector

        serves as base for:
            SVGElement
            XMLElement
            HTMLElement

HTMLElement
    basic class for all HTML els

    inherited by various HTML elements

    HTMLInputElement
        class for `<input>` els
    HTMLBodyElement
        class for `<body>`
    HTMLAnchorElement
        class for `<a>` 
    etc...

full set of props and methods of a given node comes as the result of inheritance

regular JS objects
    proptype-based classes for inheritance

`console.dir(el)` for outputting in browser
    `console.log` shows element dom tree

    `console.dir` shows the element as a DOM object

### `nodeType` Property

old-fashioned way to get the type of a DOM node

read only

numeric value
    elem.nodeType == 1 for element nodes

    elem.nodeType == 3 for text nodes

    elem.nodeType == 9 for the document object

use `instanceof` in modern scripts

### Tag: nodeName and tagName

props of DOM Node

`tagName` only exists for element nodes

`nodeName` is defined for any node
    for elements, it means the same as `tagName`

    for other node types it has a string with the node type

tagName only supported by element nodes

tag name always upper case except XHTML

### innerHTML

get HTML inside the element as a string

can modify it as well

if inserting `<script>` tag, doesn't execute

    becomes a part of HTML, just as a script that has already run

`innerHTML+=` does a full overwrite

content zeroed out and rewritten
    all images and other resources will be reloaded

### outerHTML

contains the full HTML of the el
    innerHTML + the el

writing to outerHTML does not change the el
    replaces it as a whole in ther outer context

doesn't change the el we are writitng to
    create the new content on its place instead

### nodeValue/data

innerHTML prop only valid of element nodes

other node types have `nodeValue` and `data` properties

    essentially the same

### textContent
textContent provides
access to the text inside the element

writitng to `textContent` more useful
    can write text the safe way

    with `innerHTML` inserted as HTML with all HTML tags

    with `textContent` inserted as text and all symbols are treated literally

### The 'hidden' Property

specifies if el is visible

technically works the same as `style="display:none`

### More Properties

many additional properties

`value`

`href`

`id`

# OOP

privileging data over action 

procedural programming is function oriented

data points types first
    then functions we need

JS strange because prototypal inheritance

## Class

definition of data type

field
    data

method
    functions for class

    how to act upon data

## Encapsulation

fields of instance should only be read or written by methods of instances of that class

without this, data can get passed in anywhere in code
    creates spaghetti code

public vs. private

    public methods can be accessed outside of class

    private methods can only be accessed inside class
        visible only to methods of own type

        all fields ought to be private

## Inheritance

types may overlap

subtype/supertype
    descendant/ancestor

    parent/child

good for modelling real world objects

is-a vs has-a relationship
    cat is a mammal
        inheritance
    car has a steering wheel
        composition

multiple inheritance

circular inheritance never allowed

overriding
    method in descendant

class member
    no instance passed to it

    belong to class not instance

Constructors

    set up an instance at its creation

Interface

    two classes share methods

Abstract class

    a class that doesn't mean to be instantiated

    used for inheritance

### Prototypical Inheritance

OOP without classes
    producing child instances from parent instances

# Rails Service

service layer lies between controllers and models

## What is a Service

In Domain Driven Design, service is an operation offered as an interface that stands alone in the model
    an action, not a thing

encapsulate in separate, stateless service

try to break large, domain objects doing too much work into services

## Types of Services

Application, Domain, Infrastructure

### Application Services

a service that provides non-infrastructure related operations
    don't come up when discussing the domain model outside the context of software

exporting account transactions as a CSV file 
    file format has no meaning in the domain of banking

improve cohesiveness of domain model
    prevent "software: implementation details from leakinginto it

### Domain Services

scripts a use-case involving multiple domain objects

use cases often involve rules outside the responsibility of any single obj


funds trnasfer would be an example of domain service
    doesn't quite fit in either account obj or customer

alternative approach:
    instance method on Account

CRUD are not domain services

### Infrastructure Services

encapsulate access to an external system

often used by application and domain services

emailing and message queuing

## What is a Service Layer?

application's boundary and set of available operations from the perspective of interfacing client layers
    applications's API

## Supporting Multiple Clients

most web app's API consists of simple CRUD cases

encapsulation of API allows to be used across client controllers
    thinner, more cohesive

less of benefit with rise of HTTP-based JSON APIs

## Encapsulating Application Logic

domain logic purely the problem domain

application logic technical responsibilities
    coordinating a workflow

for a more cohesive and reusable domain model, app logic should be handled by infrastructure services

app logic in domain model used by clients may have unwanted side effects

## Applying Cross-Cutting Concerns

Java web apps commonly use services to apply cross-cutting concerns
    transaction management and security

    in Spring, can write to database, send email, and enqueue message atomically

in Rails, `ActiveRecord` provides automatic transaction managemnt

## When To Use Service Layer

only reason is if have to support multiple clients using different protocols

HTTP and JSON de facto client communication protocol and format
    eliminate need for a service layer

only for client that doesn't speak HTTP

only build for today

# Flexbox

horizontal form 

# CSS Display

every element on a web page is a rectangular box

default value is inline but may resets set it to block

## Inline

`<span>`, `<em>`, `<b>`
    wrapping these els in string doesn't break the flow of the text

accept margin and padding but the el still sits inline
    only pushes other els horizontally away, not vertically

## Inline Block

set inline with natural flow of text

able to set width and height

## Block

container els usually
    `<div>`, `<section>`

    also text blocks

do not sit inline but break past them

by default, take up as much horizontal space as they can

## Run-in

doesn't work in firefox

set header el to sit inline with the text below

floating it won't work
    don't want the header to be a child of the text el bellow it

## Flexbox

## Flow-Root

new block formatting context

like a block

good for clearing floats

## Grid

## None

removes el from the page

still in the DOM, removed visually and other ways
    can't tab to it or its children

    ignored by screen readers

# CSS Positioning

for manipulating the locatino of an el

## Values

static
    evey el has a static position by default
        so that el will stick to normal page flow

    left/right/top/bottom/z-index set, then no effect on that el

relative
    el's original position remains in the flow of the doc

    left/right/top/bottom/z-index work
        nudge the el from the original position

absolute
    removed from the flow of the document and other els will behave as if its not even there

    all positional props will work on it

fixed
    el is removed from the flwo of the doc
        similar to absolute
    
    always relative tothe doc, not any particular parent and unaffected by scrolling

sticky
    like a relative value until the scroll location of the view port reaches certain threshold
        element then takes a fixed position

inherit
    position value doesn't cascade, so this forces it to


## Absolute

if child has absolute value then parent will behave as it the child isn't there at all

setting values like left, bottom, right -> child el responding to dimensions of doc not parent

to make child el positioned absolutely from its parent
    set parent position to relative

## Fixed

can help position el anywhere relative to the document, unaffected by scrolling


## Sticky

compromise bewteen the relative and fixed values

experimental and only partially adopted by select browsers

position an el relative to anything on the doc

once user scolls past certain point in the viewport
    fix the position of the el to that location

    seems persistently displayed like an element with a fixed value

# CSS Floats

CSS positioning property

like in print layout where text flows around objects

remain a part of the flow of the web page
    different that absolute positioning, which are removed

    will affectthe position of other els and other els, them

left, right, none, inherit

## Uses

can be used to create entire web layouts

can also be good for layouts in smaller instances

## Clearing the Float

float's sister prop == `clear`

an el w/ clear prop will not move up adjacted to the float

move itself down past the float

clear has four values
    both
        clears float from either direction

    left/right
        clears float from one direction respectively

    None
        default

## The Great Collapse

if parent el contained nothing but floats, the height of it collapses to nothing

fixe by clearing the float after the floated els in the container but before the close of the container

## Clearing Floats

if succeeding el consistent
    `clear: both`

Empty Div Method
    `<div style="clear: both;"></div>`
        div used bc no browser default styling

        no special function

        unlikely to be generically styled with CSS

    has no contextual meaning at all to the page and is purely for presentation
        scorned by semantic purists

Overflow Method
    setting the overflow CSS prop on a parent el

    if this prop set to auto or hidden on parent
        parent will expand to contain the floats

        clearing it for succeeding els

    if adding div just to apply this, same semantically as empty div method and less adaptable

    overflow property not specifically for clearing floats

Easy Clearing Method
    clever CSS pseudo selector `:after` to clear floats

    doesn't set overflow to parent

    apply additional calss like clear fix to it

    small bit of content hidden from view after parent el

## Problems with Floats

fragile 
    from IE 6 and slew of flat-related bugs

pushdown
    el inside a flowated item being wider than the float itself

    most browsers render the image outside the float
        stop sticking out part from affecting the layout

    IE expands float to contain image, affecting layout

    quick fix: check that images don't do this, `overflow: hidden`

Double Margin
    if margin applied in the same direction as the float, it will double the margin

    quick fix: `display: inline` on the float

3px Jog
    text set up next to a float is kicked away by 3px

    set a width or height on the affected text

Bottom Margin Bug
    if floated parent has floated children, bottom margin on those children is ignored by the parent

    use bottom padding on the parent instead

