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