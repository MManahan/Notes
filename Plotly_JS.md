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

## Class 2, Activity 2

#### Same concept as activity 1, just needed to create new datasets for the different options for the user and put them in the switch/case statement. 

## Class 2, Activity 3

#### Using d3.json to get API responses. Need the .then after the promise. 
>A promise is an object that may produce a single value some time in >the future: either a resolved value, or a reason that it’s not >resolved (e.g., a network error occurred). A promise may be in one of >3 possible states: fulfilled, rejected, or pending. Promise users can >attach callbacks to handle the fulfilled value or the reason for >rejection.
```
const url = "https://api.spacexdata.com/v2/launchpads";

// Fetch the JSON data and console log it
d3.json(url).then(function(data) {
  console.log(data);
});

// Promise Pending
const dataPromise = d3.json(url);
console.log("Data Promise: ", dataPromise);
```

## Class 2, Activity 4

#### Using d3.json to get an API response from Quandl (stock info)
#### We needed info such as name, stock, startDate, endDate and dates and closing prices from the response, or in this case "data". 
#### Each attribute can be found using the object notation and by looking at the API response. 
#### The unpack function returns an array of values given the row and index you are looking for. 
```
function unpack(rows, index) {
  return rows.map(function(row) {
    return row[index];
  });
}
```
#### In this case, dates is the first column in an array of dates. The closingPrice should be the fourth column according to the helper code, but the solved version has it as index 1. 
```
function buildPlot() {
  d3.json(url).then(function(data) {

    // Grab values from the data json object to build the plots
    var name = data.dataset.name;
    var stock = data.dataset.dataset_code;
    var startDate = data.dataset.start_date;
    var endDate = data.dataset.end_date;
    var dates = unpack(data.dataset.data, 0);
    var closingPrices = unpack(data.dataset.data, 1);
```
#### Then you build your plot off of this data like previous examples. 
```
    var trace1 = {
      type: "scatter",
      mode: "lines",
      name: name,
      x: dates,
      y: closingPrices,
      line: {
        color: "#17BECF"
      }
    };

    var data = [trace1];

    var layout = {
      title: `${stock} closing prices`,
      xaxis: {
        range: [startDate, endDate],
        type: "date"
      },
      yaxis: {
        autorange: true,
        type: "linear"
      }
    };

    Plotly.newPlot("plot", data, layout);
```
## Class 2, Acivity 5

#### Same thing as Activity 4, except we include a submission form for the user to input a stock. The script will then take the value of the form using d3. 
```
// Submit Button handler
function handleSubmit() {
  // Prevent the page from refreshing
  d3.event.preventDefault();

  // Select the input value from the form
  var stock = d3.select("#stockInput").node().value;
  console.log(stock);

  // clear the input value
  d3.select("#stockInput").node().value = "";

  // Build the plot with the new stock
  buildPlot(stock);
}
```
#### The code above calls the function buildPlot that is the same as activity 4. You just need to pass in the stock value from the input form. 

## Class 3, Activity 1

#### Bringing back Flask. Running the app.py to run the server. The html code has the plot code built in to the script element. The home route renders the html file, the /line route shows the data as a json file. 

## Class 3, Activity 2

#### Here we used two python scripts. 
- One to run the Flask server (app.py) and one for the lyrics.py. 
- The lyrics.py creats a function get_lyrics() that opens a text file and using .strip() strips the empty spaces creating an array of lyric lines. The "Counter" module is imported. 
#### This Counter takes each line in the array of lyrics and sets it as a key and the amount of times the lyric shows up is the value. The Counter(lyrics) returns a dictionary. 
```
from collections import Counter


def get_lyrics():
    with open('lyrics.txt') as fh:
        lyrics = [line.strip() for line in fh if line.strip()]
        return Counter(lyrics)


if __name__ == '__main__':
    lyrics = get_lyrics()
    labels, values = zip(*lyrics.items())

    print(labels, values)
```
#### The app.py script runs the server with the home or ("/") route rendering the index.html. 
#### The ("/pie) route is the endpoint that displays the jsonified data. The function rick() does the following:
1. First it sets the get_lyrics() function to a variable, which as mentioned above, returns a dictionary
2. Then use zip to unzip the dictionary into the labels and values. In this case, labels are the words and values are the amount of times those words showed up. 
3. type is set to pie
4. returns the jsonified data. 
```
from lyrics import get_lyrics

from flask import Flask, jsonify, render_template
app = Flask(__name__)


@app.route("/")
def index():
    return render_template('index.html')


@app.route("/pie")
def rick():

    lyrics = get_lyrics()
    labels, values = zip(*lyrics.items())
    data = [{
        "labels": labels,
        "values": values,
        "type": "pie"}]

    return jsonify(data)


if __name__ == "__main__":
    app.run(debug=True)
```

#### The html file then uses d3.json(url) to get the response from the API endpoint. In this case, url = /pie. When you access the endpoint, it should give the json dictionary of the unzipped lyrics.
#### Plotly is then used to plot the data in the front end. 
```
<body>
    <div id="pie"></div>
    <script>
        var url = "/pie";
        d3.json(url).then(function(data){
            var layout = {
                title: "Lyric Frequency"}
            Plotly.plot("pie", data, layout);
        });
    </script>
</body>
```

## Class 3, Acitivity 4

#### Puts Flask(server), Javascript(plotly), SQLAlchemy(database), D3 and html together.  

### app.py notes

- Use Boiler Plate SQL Alchemy set up code. Set "app" as the Flask instance. Then config "app" to access the bigfoot sqlite database. Set db to that database to be able to access it. 
- Create the schema for the BigFoot table. Open up the table in tabluePlus or PostGres to see what the columns are and what their datatypes are. 
- Create the database classes
```
# Create database classes
@app.before_first_request
def setup():
    # Recreate database each time for demo
    # db.drop_all()
    db.create_all()
```
- Set the (home) page or the ("/") route to render the html file. Need to use render_template function that we imported from Flask
```
# Create a route that renders index.html template
@app.route("/")
def home():
    return render_template("index.html")
```
- Then we query the database to be able to plot how many bigfoot sightings per year. 
```
# Query the database and return the jsonified results
@app.route("/data")
def data():
    sel = [func.strftime("%Y", Bigfoot.timestamp), func.count(Bigfoot.timestamp)]
    results = db.session.query(*sel).\
        group_by(func.strftime("%Y", Bigfoot.timestamp)).all()
    df = pd.DataFrame(results, columns=['year', 'sightings'])
    return jsonify(df.to_dict(orient="records"))
```
- The func.strftime("%Y", Bigfoot.timestamp) returns the year from the timestamp. 

#### Essentially, we set the variable "sel" for our query which are years and the count of the years. 
```
    sel = [func.strftime("%Y", Bigfoot.timestamp), func.count(Bigfoot.timestamp)]
```
- Then we pass the results into a dataframe and set the columns to "year" and "sightings"
```
df = pd.DataFrame(results, columns=['year', 'sightings'])
```
- We then return a jsonified file where we pass the dataframe into a dictionary. Orient sets the type of json string format. According to the documentation, it will return 

> ‘columns’ : dict like {column -> {index -> value}}

#### if you navigate to the ("/data") route, you will see the jsonfied data is an array of objects with key value pairs. 

### app.js notes

#### This app.js script is what plots the data. It uses the endpoint of ("/data"). 

#### Creates a function buildPlot() to build the plots
- use d3.json to get the response from the /data endpoint. This is where we hear about the "promise" and "then" stuff. 
```
function buildPlot() {
  d3.json(url).then(function(response) {
```
- So after it gets the response of collecting the data from the /data endpoint, it prints the data in console, but also creates the trace from the response
- The trace sets the "type", "mode", "name", x-values, y-values and line color. 
```
    type: "scatter",
      mode: "lines",
      name: "Bigfoot Sightings",
      x: response.map(data => data.year),
      y: response.map(data => data.sightings),
      line: {
        color: "#17BECF"
      }
    };
```
#### For each x value, you need to map the year, so we use the .map function. 
> Remember: .map function creates an array after the call back function does something to each element of that array. 

#### In this case, we are trying to get the year for the x values and the number of sightings for the y values. Essentially, the x and y values are not set to arrays of years for x and number of sightings for y. 

- Next we set the data by making trace an array. 
>var data = [trace];

### Why?

> The newplot documentation says it expects data to be an array of objects. With out the [] around trace, it is only an object. [trace] is now an array of that object. 

- Set the layout to include the title, xlabel, y lable then plot. 

#### The first parameter to pass into newPlot is the html element where we want to plot to. If you go back to index.html, we want to plot it in the div with id "plot".