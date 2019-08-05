# Plotly.JS Notes
## Class 1, Activity 1

#### Went over "let", "var" and "const". Setting the "var" AFTER you call the variable returns "undefined". When you do the same thing with  "let", it returns a Reference error. This is because JS "lifts" variables up to the top. 
#### "Const" assignments cannot be re-assigned, but they can still be manipulated if it is an object or array. 

## Class 1, Activity 2

#### Started Plotly.newPlot
#### Set "trace" as a variable to hold the object that will be passed into Plotly.newPlot
#### Plot.newPlot(graphDiv, data, layout)

- graphDiv = the element the plot will be displayed in the html file
- data is the object(trace) that holds, x, y and type of graph. It is expected to be an <b><u>ARRAY</u></b>
- layout adds the attributes of the chart, like title and x&y axis labels

### Example of trace, layout and Plotly.newPlot():
```
var trace1 = {
  x: ["beer", "wine", "martini", "margarita",
    "ice tea", "rum & coke", "mai tai", "gin & tonic"],
  y: [22.7, 17.1, 9.9, 8.7, 7.2, 6.1, 6.0, 4.6],
  type: "scatter"
};
var trace2 = {
  x: ["beer", "wine", "martini", "margarita",
    "ice tea", "rum & coke", "mai tai", "gin & tonic"],
  y: [22.7, 17.1, 9.9, 8.7, 7.2, 6.1, 6.0, 4.6],
  type: "scatter"
};
var data = [trace1,trace2];

var layout = {
  title: "'Bar' Chart"
};

Plotly.newPlot("plot", data, layout);
```
## Class 1, Activity 3

#### var eyeColor was defined as an array of eyeColors. eyeFlicker was defined as an array of flicks. var trace was then defined to set x : eyeColor and y : eyeFlicker with the type : "bar". 
#### layout - title, xaxis and yaxis was defined. x&y axis are defined as objects. 
```
var layout = {
  title: "Eye Color vs Flicker",
  xaxis: { title: "Eye Color" },
  yaxis: { title: "Flicker Frequency" }
};
```
## Class 1, Activity 4

#### Just showed that you can pass multiple traces into data. It will plot both sets of data in the same graph
```
var data = [trace1, trace2];
```

## Class 1, Activity 5

#### Data.js provided data of greek/roman names and search results. Needed to plot the "pair" as the x-axis and greek/roman SearchResults as the y - axis
#### so trace one should be x : "pair" and y : "greek/roman SearchResults"
#### Since data is given as an array of objects, need to use the map function to create an new array for the x and y values we want. *REMEMBER* that the map function creates a new array based on the function that you call on the array. In this case, we just want to get the object value 
- name = sets the trace name. The trace name appears as the legend item when you hover over it. 
- text = sets the text elements that are associated with each x,y pair

## Class 1, Activity 6 

#### Covered slicing of arrays again using their index numbers
```
// Array of names
const names = ["Jane", "John", "Jimbo", "Jedediah"];

// Slices first two names
const left = names.slice(0, 2);
console.log(left);

// Slices last two names and return
const right = names.slice(2, 4);
console.log(right);
```
#### Also covered sort function. The sort function works well for strings. It sorts it alphabetically. 
#### For numeric sorts, you need to use the Compare function(a,b), then set the function to return a-b or b-a depending if you want to sort by ascending or descending order. In this case, a = firstNum, b = secondNum

- DESCENDING Sort
```
// Sorts descending
[3, 2, -120].sort(function compareFunction(firstNum, secondNum) {
   // resulting order is (3, 2, -120) 
  return secondNum - firstNum;
});
```
- ASCENDING Sort
```
// Sorts ascending
[3, 2, -120].sort(function compareFunction(firstNum, secondNum) {
  // resulting order is (-120, 2, 3)
  return firstNum - secondNum;
});

// Arrow Function
[3, 2, -120].sort((first, second) => first - second);
```

## Class 1, Activity 7

#### Covered Horizontal Bar graphs plus the use of sort and accessing data objects values. 
#### We sorted the greekSearchResults data in Descending order by:
```
// Sort the data array using the greekSearchResults value
data.sort(function(a, b) {
  return parseFloat(b.greekSearchResults) - parseFloat(a.greekSearchResults);
});
```
#### The object notation grabs the greekSearchResults value and turns it into a float data type. Initially it was a string. 

## Class 2, Activity 1

#### This activity shows us how to create a drop down option for datasets to plot. What the user sees is the plot and a drop down menu with 4 datasets. The plot.js script initializes the initial graph on load, which is just a line on the x-axis. 
#### The HTML file has a "select" element with option children for each option the user can select. 
```
<select id="selDataset" onchange="getData(this.value)">
    <option>---</option>
    <option value="dataset1">DataSet1</option>
    <option value="dataset2">DataSet2</option>
    <option value="dataset3">DataSet3</option>
  </select>
  ```
#### The on-change this.value gets the value of what the user chose. In this case, there are 3 choices, dataset1, dataset2 and dataset3. This value is then passed into the "getData" function which is coded in plot.js. 
1. The getData function sets an empty array for x and y
2. Then has a switch/case statement to figure out which dataset to use based on the users drop down choice. 
3. It then passes the x and y arrays into the "updatePlotly" function which restyles the plot to show the dataset the user chose. 