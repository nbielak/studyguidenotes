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

## Subqueries in Conditional Logic
