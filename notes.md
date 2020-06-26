# Notes

- D3, a JavaScript-based tool for loading data into a web page and generating visuals from that data.
- https://alignedleft.com/resources/data-vis-jobs
- Visualizing data is the fastest way to communicate it to others.
- Revealing unexpected patterns and trends in the otherwise hidden information around us. At its best, data visualization is expert storytelling.
- Visualization is a process of mapping information to visuals. We craft rules that interpret data and express its values as visual properties

- Dynamic, interactive visualizations can empower people to explore the data for themselves.
- interactivity can also encourage engagement with the data in ways that static images cannot.
- Some visualizations can make exploring data feel more like playing a game. Interactive visualization can be a great medium for engaging an audience who might not otherwise care about the topic or data at hand.

- The more accessible your visualization, the greater your audience and your impact

- Because D3 is written in JavaScript, learning to use D3 often means learning a lot about JavaScript.



### Introducing d3
- D3 is an elegant piece of software that facilitates generation and manipulation of web documents with data.
1. Loading data into the browser’s memory
2. Binding data to elements within the document, creating new elements as needed
3. Transforming those elements by interpreting each element’s bound datum and setting its visual properties accordingly
4. Transitioning elements between states in response to user input
- You provide the concept, you craft the rules, and D3 executes it—without telling you what to do.
- D3 doesn’t hide your original data. D3 code is executed on the client side, the data you want visualized must be sent to the client. If your data can’t be shared, then don’t use D3
- paper.js


### Technology Fundamentals
- HTML : Class and ID names cannot begin with numerals; they must begin with alphabetic characters.The browser will not give you any errors; your code simply won’t work.
- Rendering: to a browser, everything is a box.
- Styles, Inheritance, Cascading, and Specificity: 
    - Inheritance is a great feature of CSS, as children adopt the styles of their parents. 
    -  When more than one selector applies to an element, the later rule generally overrides the earlier one.
    - Later rules generally override earlier ones, but not always. The true logic has to do with the specificity of each selector. If two selectors have the same specificity, then the later one will be applied.
    - To save yourself headaches later, keep your selectors clear and easy to read. Start with general selectors on top, and work your way down to more specific ones, and you’ll be all right.
- Javascript: 

```
    typeof 67;              //Returns "number"
    var myName = "Scott";
    typeof myName;          //Returns "string"
    myName = true;
    typeof myName;          //Returns "boolean"
```

- python -m SimpleHTTPServer

## Data
- Data is structured information with potential for meaning
- Whatever your data, it can’t be made useful and visual until it is attached to something. In D3 lingo, the data must be bound to elements within the page.

- Many, but not all, D3 methods return a selection (actually, a reference to a selection), which enables this handy technique of method chaining. Typically, a method returns a reference to the element that it just acted on, but not always.

- With D3, we bind our data input values to elements in the DOM. Binding is like “attaching” or associating data to specific elements, so that later you can reference those values to apply mapping rules. Without the binding step, we have a bunch of data-less, unmappable DOM elements. No one wants that.


### loading data
- csv() takes two arguments: a string representing the path of the CSV file to load in, and an anonymous function to be used as a callback function. The callback function is “called” only after the CSV file has been loaded into memory. So you can be sure that, by the time the callback is called, d3.csv() is done executing.

d3.select("body").selectAll("p")
            .data(dataset)
            .enter()
            .append("p")
            .text("New paragraph!");

- Here’s what’s happening:

d3.select("body")
Finds the body in the DOM and hands off a reference to the next step in the chain.

.selectAll("p")
Selects all paragraphs in the DOM. Because none exist yet, this returns an empty selection. Think of this empty selection as representing the paragraphs that will soon exist.

.data(dataset)
Counts and parses our data values. There are five values in our array called dataset, so everything past this point is executed five times, once for each value.

.enter()
To create new, data-bound elements, you must use enter(). This method looks at the current DOM selection, and then at the data being handed to it. If there are more data values than corresponding DOM elements, then enter() creates a new placeholder element on which you can work your magic. It then hands off a reference to this new placeholder to the next step in the chain.

.append("p")
Takes the empty placeholder selection created by enter() and appends a p element into the DOM. Hooray! Then it hands off a reference to the element it just created to the next step in the chain.

.text("New paragraph!")
Takes the reference to the newly created p and inserts a text value.

## Drawing with data
- attr() sets DOM attribute values, whereas style() applies CSS styles directly to an element.

### drawing svgs
- Another value, i, is also automatically populated for us.
- i is a numeric index value of the current element. 
- To make sure i is available to your custom function, you must include it as an argument in the function definition, function(d, i)


### Making a bar chart
- With D3, you always have to first select whatever it is you’re about to act on, even if that selection is momentarily empty


## Scales
- Scales are functions that map from an input domain to an output range
- The values in any dataset are unlikely to correspond exactly to pixel measurements for use in your visualization. Scales provide a convenient way to map those data values to new values useful for visualization purposes.
- D3 scales are functions with parameters that you define. Once they are created, you call the scale function and pass it a data value, and it nicely returns a scaled output value. You can define and use as many scales as you like.
- A scale is a mathematical relationship, with no direct visual output. I encourage you to think of scales and axes as two different, yet related, elements.

### Domains and ranges
- A scale’s input domain is the range of possible input data values
- A scale’s output range is the range of possible output values, commonly used as display values in pixel units.
- Normalization: the process of mapping a numeric value to a new value between 0 and 1, based on the possible minimum and maximum values.

d3 max for simple datasets:

```
var simpleDataset = [7, 8, 4, 5, 2];
d3.max(simpleDataset);  // Returns 8
```

### Time scales
- JavaScript and D3 can only perform time and date calculations on Date objects, not on strings
- working with dates in D3 involves:
    - Converting strings to Date objects
    - Using time scales, as needed
    - Formatting Date objects as human-friendly strings, for display to the user.


### Axis
- D3’s axes are functions whose parameters you define. When an axis function is called, it doesn’t return a value, but generates the visual elements of the axis, including lines, labels, and ticks.
-  A g element is a group element. Group elements are invisible yet  can be used to containother elements. And we can apply transformations to g elements, which affects how visual elements within that group are rendered.
- D3’s call() function takes the incoming selection, as received from the prior link in the chain, and hands that selection off to any function.

## Transitions
- Updates: changes in data
- Ordinal scales are typically used for ordinal data, usually categories with some inherent order to them
- To set the domain of an ordinal scale, you typically specify an array with the category names
- there is a very simple way to quickly generate an array of sequential numbers: the d3.range() method.
- ordinal scales (like d3.scaleBand()) use discrete ranges, meaning the output values are determined in advance, and could be numeric or not.

### Updating data
- Make sure to always set an initial value before attempting to transition to a new value.

- by default, only one transition can be active on any given element at any given time

- on("end", …), however, is a good place to specify additional transitions, because by the time on("end", …) is called, the primary transition has already ended, so initiating a new transition won’t cause any harm.

- there is an even simpler way to schedule multiple transitions to run one after the other: we simply chain transitions together. Instead of reselecting elements and calling a new transition on each one with on("end", …), just tack a second transition onto the end of the chain.

### Adding values
- The data() method also returns a selection. Specifically, data() returns references to all elements to which data was just bound, which we call the update selection.
- we can use merge() to combine that enter selection with the update selection (the old, preexisting rects).

### Removing values
- Whenever there are more DOM elements than data values, the exit selection contains references to those elements without data.
- remove() is a special transition method that waits until the transition is complete, and then deletes the element from the DOM forever.
- Visually speaking, it’s good practice to perform a transition first, rather than simply remove() elements right away.


### Data Joins with Keys
- A data join happens whenever you bind data to DOM elements; that is, every time you call data().
- The default join is by index order, meaning the first data value is bound to the first DOM element in the selection, the second value is bound to the second element, and so on.
- We can use a key function to control the data join with more specificity and ensure that the right datum is bound to the right rect element.
- When we’re binding data, now the index order will be ignored; the key values will be used instead. This is what gives us the flexbility to add and remove data values (and elements) arbitrarily—as long as each one has a unique key.



## Interactivity
- Events don’t happen in a vacuum. Rather, they are always called on a specific element.
- You can bind event listeners right at the moment when you first create elements.
- A simple hover effect can be achieved with CSS alone—no JavaScript required!

### click to sort
- Interactive visualization is most powerful when it can provide different views of the data, empowering the user to explore the information from different angles.
- sort() method, which reorders elements within the selection based on their bound data values. sort() needs to know how to decide which elements come first, and which later, so we pass into it a comparator function.
- it is passed two values, a and b, which represent the data values of two different elements. (You could name them anything else; a and b are just the convention.) The comparator will be called on every pair of elements in our array, comparing a to b, until, in the end, all the array elements are sorted per whatever rules we specify.
- Another way to prevent transition interruptions is to name your transitions. Named transitions can operate concurrently and don’t conflict with each other, assuming they’re not trying to modify the same attributes.



## Using paths
- path elements are SVG’s answer to drawing irregular forms. Anything that’s not a rect, circle, or another simple shape can be drawn as a path

### Dealing with missing data
Or we could leave the data untouched, and use the line generator’s defined() method to determine, on the fly, whether or not each individual value is defined (or valid). defined() is just another configuration method, like x() and y(). If the result of its anonymous function is true, then that data value is included. If not, the value is excluded.



# Layouts
- D3 layouts take data that you provide and remap or otherwise transform it, thereby generating new data that is more convenient for a specific visual task

## Pie layout
- To draw those pretty wedges, we need to know a number of measurements, including an inner and outer radius for each wedge, plus the starting and ending angles.

- The pie layout takes our simple array of numbers and generates an array of objects, one object for each value. Each of those objects now has a few new values—most important, startAngle and endAngle.+

- Arcs are defined as custom functions, and they require inner and outer radius values