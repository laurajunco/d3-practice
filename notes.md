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


### Making a Scatterplot