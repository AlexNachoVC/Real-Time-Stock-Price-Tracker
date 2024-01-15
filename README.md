# Real-Time Stock Price Tracker

## Project Description

This project is a real-time stock price tracker that fetches and displays the current stock prices of specified ticker symbols. This application allows users to track the prices of their favorite stocks. Users can add and remove stocks, and the prices are updated every 15 seconds.

## Features

- Real-time tracking of stock prices
- Supports multiple ticker symbols
- Color-coded price changes for easy visualization

## How to Use

1. Clone the repository to your local machine.
2. Navigate to the project directory.
3. Run `flask run` to start the server.
4. Open a web browser and navigate to `http://127.0.0.1:5000` to view the application.

## File Explanations

### `app.py` 

This is the main server file for the application. It uses the Flask framework to handle HTTP requests and responses.

- `yfinance` is imported to fetch stock data.
- `Flask`, `request`, `render_template`, and `jsonify` are imported from the `flask` package to handle HTTP requests and responses, render HTML templates, and convert Python objects to JSON, respectively.

The application is initialized with `app = Flask(__name__, template_folder='templates')`.

There are two routes defined:

1. `'/'` (GET): This route renders the `index.html` template when the root URL of the server is accessed.

2. `'/get_stock_data'` (POST): This route fetches stock data for a given ticker symbol. The ticker symbol is extracted from the JSON body of the POST request with `request.get_json()['ticker']`. The `yfinance` package is used to fetch the stock data. The current and opening prices of the stock are returned as a JSON response.

The server is run with `app.run(debug=True)` if the script is run directly (i.e., it is not imported as a module). The `debug=True` argument means that the server will automatically reload if code changes are detected, and it will provide detailed error messages if an error occurs.



### `script.js` 

This is the main JavaScript file for the application. It handles the dynamic functionality of the web page, including fetching and displaying stock data, and updating the data at regular intervals.

#### Variables

- `tickers`: An array that stores the ticker symbols of the stocks to track. It is initialized with the ticker symbols stored in local storage, or an empty array if no ticker symbols are stored.

- `lastPrices`: An object that stores the last known prices of the stocks. It is used to compare the current price of a stock with its last known price to determine whether the stock price has increased, decreased, or stayed the same.

- `counter`: A variable that counts down from 15 to 0. When it reaches 0, the stock prices are updated.

#### Functions

- `startUpdateCycle()`: Starts the update cycle for the stock prices. It immediately updates the prices and then starts a timer that counts down from 15 to 0. When the counter reaches 0, the prices are updated again.

- `addTickerToGrid(ticker)`: Adds a new ticker symbol to the grid on the web page.

- `updatePrices()`: Updates the prices for all ticker symbols in the `tickers` array. It makes a POST request to the `/get_stock_data` endpoint for each ticker symbol, calculates the percentage change in the stock price, determines the color class to use for the price and percentage change, updates the text and color of the price and percentage change elements, determines the flash class to use for the ticker symbol, updates the last known price, and adds and removes the flash class from the ticker symbol element to create a flashing effect.

#### Event Handlers

- `$(document).ready(function() {...})`: Runs when the HTML document has finished loading. It adds each ticker symbol in the `tickers` array to the grid, updates the stock prices, and sets up an event handler for the "submit" event of the form to add a new ticker symbol.

- `$("#tickers-grid").on("click", ".remove-btn", function() {...})`: Runs when an element with the class of "remove-btn" inside the element with the ID of "tickers-grid" is clicked. It removes the associated ticker symbol from the `tickers` array and the grid.

- `$("#add-ticker-form").submit(function(e) {...})`: Runs when the form to add a new ticker symbol is submitted. It prevents the form from being submitted normally, gets the ticker symbol entered by the user, and adds it to the `tickers` array and the grid if it is not already in the `tickers` array.



### `index.html` 

This is the main HTML file for the application. It defines the structure of the web page and includes links to the CSS and JavaScript files.

#### Elements

- `<!DOCTYPE html>`: This declaration defines the document type and version of HTML.

- `<html lang="en">`: This is the root element of the HTML document and the value of the `lang` attribute is `en` which stands for English.

- `<head>`: This element contains meta information about the HTML document and links to the CSS and JavaScript files.

- `<meta charset="UTF-8">`: This element specifies the character encoding for the HTML document.

- `<title>Stock Price Tracker</title>`: This element defines the title of the HTML document.

- `<link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">`: This element links the CSS file to the HTML document.

- `<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>`: This element includes the jQuery library in the HTML document.

- `<script src="{{ url_for('static', filename='script.js') }}"></script>`: This element includes the JavaScript file in the HTML document.

- `<body>`: This element contains the content of the HTML document.

- `<form id="add-ticker-form">`: This form is used to add a new ticker symbol. It contains an input field and a submit button.

- `<p id="timer">`: This paragraph displays the countdown to the next update of the stock prices.

- `<div id="tickers-grid">`: This div element is used to display the grid of ticker symbols and their prices.


### `style.css` 

This is the main CSS file for the application. It defines the styles for the HTML elements.

#### Styles

- `#tickers-grid`: This style applies to the HTML element with the ID of "tickers-grid". It sets the element to display as a flex container and allows the flex items to wrap onto multiple lines.

- `.stock-box`: This style applies to any HTML elements with the class of "stock-box". It sets the width and height of the elements to 200px, the border to a 1px solid line with the color #333, the margin to 10px, the padding to 10px, the background color to #eee, and the transition for the background color to 0.5s.

- `.light-red`, `.dark-red`, `.grey`, `.dark-green`, `.light-green`: These styles apply to any HTML elements with the corresponding class. They set the color of the text in the elements to the specified color.

Please note that the `#tickers-grid` and `.stock-box` styles are duplicated in the provided code snippet. This could be a mistake, and you might want to remove the duplicate styles.


## Technologies Used

- Python
- Flask
- JavaScript
- jQuery
- HTML/CSS

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)