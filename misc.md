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

