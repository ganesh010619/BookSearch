# Book Search Application

## Overview

The **Book Search Application** is a simple web tool that allows users to search for books based on criteria such as title, author, category, publisher, and price range. The application makes it easy for users to find and view books, as well as filter results by their preferred price range. The backend is built using **Flask** and the application uses **Elasticsearch** to store and retrieve book data.

## Features

- **Search for Books:**
  - Search by **title**, **author**, **category**, or **publisher**.
  - Filter results by **price range** (Min Price, Max Price).
  - View detailed book information like **author**, **category**, **publisher**, and **price**.

- **Easy-to-Use Interface:**
  - The app provides a clean, user-friendly interface to search and filter books.
  - Results are displayed dynamically as you interact with the search form.

- **Current Location Detection (optional feature)**: Automatically detects the user's location and adjusts the search radius for better results (if enabled).

## Requirements

- **Python**: Version 3.6 or higher
- **Elasticsearch**: Version 8.x
  - **Ports Used**:
    - Elasticsearch runs on `http://localhost:9200`
    - Flask backend runs on `http://localhost:8000`

- **Libraries**:
  - **Elasticsearch**: For storing and querying book data.
  - **Flask**: Backend API development for managing search requests and interacting with Elasticsearch.
  - **Frontend (HTML/CSS/JS)**: The user interface that allows users to search and view books, built with basic HTML, CSS, and JavaScript.
  - **JavaScript `fetch()` API**: Used in the frontend to send HTTP requests to the Flask API.

## Step-by-Step Instructions

### 1. Install Elasticsearch

- **Download Elasticsearch** from the [official website](https://www.elastic.co/downloads/elasticsearch).
- **Start Elasticsearch** by running the following command in the terminal (after unzipping the package):

```bash
./bin/elasticsearch
```

### 2. Load Data into Elasticsearch

- Open the file `index_data.py` and verify the Elasticsearch host and port are correctly set.
- This script will load book data into Elasticsearch, ensuring that data is properly indexed and searchable.
- Run the script:

```bash
python index_data.py
```

### 3. Run the Backend Server

- The backend is powered by **Flask**, which handles API requests from the frontend and interacts with **Elasticsearch** to fetch data.
- Open the file `app.py` and ensure the Elasticsearch host and port are correctly set.
- Run the Flask backend server by executing the following command in the terminal:
- 
```bash
python app.py
```
- Verify that the backend is running by visiting http://localhost:8000 in your browser.

### 4. Run the Frontend Application

- The frontend is built using **HTML**, **CSS**, and **JavaScript**. It communicates with the backend to display search results.
- Open `index.html` in your browser. The app will allow you to search for books and display results dynamically as you interact with the search form.
- The frontend uses **JavaScript's `fetch()` API** to make requests to the Flask backend (`http://localhost:8000`).

## Usage Instructions

### 1. Search for Books

1. Open the **Search Page** in your web browser.
2. Enter search terms in the available fields:
   - **Title**: Search for books by their title.
   - **Author**: Search for books by the author's name.
   - **Category**: Search for books by category (e.g., Fiction, History).
   - **Publisher**: Search for books by the publisher.
3. Optionally, set a **Price Range** filter by entering values for the minimum and maximum price:
   - **Min Price**: Set the minimum price for the books you want to see.
   - **Max Price**: Set the maximum price for the books you want to see.
4. Press the **Search** button to retrieve the list of books that match your search criteria.

### 2. Filter by Price

1. To filter results by price, you can set a **Minimum Price** and/or **Maximum Price**:
   - **Min Price**: Set the lowest price you are willing to pay.
   - **Max Price**: Set the highest price you are willing to pay.
2. After setting the price filters, the results will automatically update to show only the books within the specified price range.

### 3. View Book Details

1. Once you perform a search, a list of books will be displayed on the screen based on your search criteria.
2. Click on any book from the list to view its detailed information, such as:
   - **Title**: The title of the book.
   - **Author**: The author(s) of the book.
   - **Category**: The category or genre of the book (e.g., Fiction, Cooking).
   - **Publisher**: The publisher of the book.
   - **Price**: The price of the book.
3. All of these details will be displayed in a clear, easy-to-read format.

### 4. Modify Search Criteria

1. To modify your search, you can update the fields (title, author, category, publisher, or price range) and click **Search** again.
2. The search results will update based on the new criteria.

### 5. Error Handling and Messages

- **No Results Found**: If no books match your search criteria, a message saying "No results found." will be displayed.
- **Invalid Search**: If there is an issue with the search input (such as an empty search or invalid characters), the backend will return an appropriate error message.

---

## Example Usage Scenarios:

### Example 1: Search by Title and Author

1. Enter **"The Great Gatsby"** in the **Title** field.
2. Enter **"F. Scott Fitzgerald"** in the **Author** field.
3. Click **Search**.
4. The application will show books that match the title "The Great Gatsby" and were authored by "F. Scott Fitzgerald."

### Example 2: Filter by Price Range

1. Enter **"Science Fiction"** in the **Category** field.
2. Set **Min Price** to `10` and **Max Price** to `30`.
3. Click **Search**.
4. The application will show books in the "Science Fiction" category priced between $10 and $30.

---

## Troubleshooting

- **Elasticsearch Connection Error**:
  - If you encounter errors like "Could not connect to Elasticsearch", make sure Elasticsearch is running on `http://localhost:9200`.
  - To start Elasticsearch, use the following command:

    ```bash
    ./bin/elasticsearch
    ```

  - Ensure there are no firewall or network issues blocking the connection.

- **Data Not Loaded**:
  - If no data is appearing in the search results, you may need to reload the data into Elasticsearch. To do so, run the `index_data.py` script:

    ```bash
    python index_data.py
    ```

- **Search Returns Incomplete or Incorrect Results**:
  - Check if the query logic in the `app.py` file is correctly handling filters and search criteria.
  - Verify that the field names match those in the Elasticsearch index.
  - You can check the mapping of the `books` index with this command:

    ```bash
    curl -X GET "http://localhost:9200/books/_mapping?pretty"
    ```

- **Frontend Display Issues**:
  - Open the browser's developer console (press `F12`) to check for JavaScript errors.
  - Ensure the Flask backend (`app.py`) is running at `http://localhost:8000`.
  - Make sure the frontend is correctly calling the backend API.

- **Missing Data or Empty Search Results**:
  - If certain books are missing, check that the data in `books.json` is structured correctly and matches the expected format for Elasticsearch.
  - Run `index_data.py` to reload the data if necessary.

- **CORS Issues**:
  - If you encounter CORS issues, ensure CORS is enabled on the Flask backend:

    ```python
    from flask_cors import CORS
    CORS(app)  # Enable CORS
    ```

---

## Key Files

- **`index_data.py`**: Loads data into Elasticsearch and defines the mapping for the `books` index.
- **`app.py`**: Flask backend that interacts with Elasticsearch and handles API requests.
- **`index.html`**: The frontend HTML file that allows users to search for books and view results.
- **`styles.css`**: The CSS file used to style the frontend interface.

---

## Screenshots

### Search Interface:
![Search Interface](./images/search-interface.png)

### Search Results:
![Search Results](./images/search-results.png)

### Book Details Page:
![Book Details](./images/book-details.png)
