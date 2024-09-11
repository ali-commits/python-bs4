# Introduction to Web Scraping with Requests and Beautiful Soup

## What is Web Scraping?
Web scraping is the process of automatically extracting data from websites. It's like having a robot assistant that can quickly read and collect information from web pages for you.

## What is Beautiful Soup?
Beautiful Soup is a Python library that makes web scraping easy and intuitive. It helps you navigate and search through HTML and XML files, allowing you to extract the specific information you need from web pages.

## Why Learn Beautiful Soup?
1. Extract data from websites for analysis
2. Automate data collection tasks
3. Build datasets for machine learning projects
4. Monitor websites for changes
5. Create price comparison tools

# Introduction to Requests

## What is Requests?
Requests is a popular Python library used for making HTTP requests. It abstracts the complexities of making requests behind a simple API, allowing you to send HTTP/1.1 requests easily. With Requests, you have the power to interact with web services and retrieve web page content effortlessly.

## Why Use Requests?
1. Simple and intuitive API
2. Automatic decompression of response content
3. Connection pooling for better performance
4. Built-in JSON decoding
5. Session cookie persistence
6. Support for multipart file uploads
7. Automatic content decoding


## Setting Up Your Environment

### Step 1: Install Python

1. Visit the official Python website: https://www.python.org/downloads/
2. Download the latest version of Python 3 (e.g., Python 3.9 or later)
3. Run the installer:
   - On Windows, make sure to check the box that says "Add Python to PATH"
   - On macOS and Linux, the installer should set up the PATH automatically

Verify the installation by opening a command prompt or terminal and typing:
```
python --version
```



### Step 3: Install Required Packages

With your virtual environment activated (if you're using one), install the required packages:

```
pip install beautifulsoup4 requests
```

### Step 4: Verify Installation

Create a new file called `test_bs4.py` with the following content:

```python
import requests
from bs4 import BeautifulSoup

response = requests.get('https://www.python.org')
soup = BeautifulSoup(response.text, 'html.parser')
print(soup.title.string)
```

Run the script:
```
python test_bs4.py
```

If everything is set up correctly, you should see the title of the Python.org homepage printed.


## Basic Usage of Requests

## Example 1: Basic HTML Parsing

```python
from bs4 import BeautifulSoup

html_doc = """
<html>
  <head><title>My First Web Page</title></head>
  <body>
    <h1>Welcome to Web Scraping</h1>
    <p class="intro">This is an introduction to Beautiful Soup.</p>
    <p>It's going to be <b>awesome</b>!</p>
  </body>
</html>
"""

soup = BeautifulSoup(html_doc, 'html.parser')

print(soup.title.string)
print(soup.h1.string)
print(soup.find('p', class_='intro').string)
```

### Example 2: Making a GET request

```python
import requests

# Make a GET request to a web page
response = requests.get('https://www.example.com')

# Check the status code
print(f"Status code: {response.status_code}")

# Print the content of the page
print(response.text[:500])  # Print first 500 characters

# Print the headers
print(response.headers)
```

### Example 3: Passing Parameters in URLs

```python
import requests

# Make a GET request with parameters
params = {'key1': 'value1', 'key2': 'value2'}
response = requests.get('https://httpbin.org/get', params=params)

# Print the URL that was actually requested
print(response.url)

# Print the content of the response
print(response.text)
```

### Example 3: Making a POST request

```python
import requests

# Make a POST request
data = {'username': 'example', 'password': 'password123'}
response = requests.post('https://httpbin.org/post', data=data)

# Print the response content
print(response.text)

# If the response is JSON, you can access it like a dictionary
json_response = response.json()
print(json_response['form'])  # Print the form data that was sent
```

## Combining Requests with Beautiful Soup

Now that we've covered both Requests and Beautiful Soup, let's see how they work together:

```python
import requests
from bs4 import BeautifulSoup

# Make a request to a web page
url = 'https://news.ycombinator.com/'
response = requests.get(url)

# Create a BeautifulSoup object and specify the parser
soup = BeautifulSoup(response.text, 'html.parser')

# Use Beautiful Soup to parse the content
headlines = soup.find_all('span', class_='titleline')

# Print the first 5 headlines
for headline in headlines[:5]:
    print(headline.text)
```

This example demonstrates how Requests is used to fetch the web page content, which is then parsed using Beautiful Soup.

# Exercises


1. **Basic Parsing**: Create a BeautifulSoup object from a given HTML string and extract:
   - The text of all `<h2>` tags
   - The href attribute of all `<a>` tags
   - The text of the third `<p>` tag

2. **Simple Scraper**: Write a script that scrapes a weather website (e.g., weather.com) and prints:
   - The current temperature
   - Today's weather description (e.g., "Partly Cloudy")
   - Tomorrow's forecast

3. **Data Extraction**: Scrape a book listing website (e.g., books.toscrape.com) and create a list of dictionaries containing:
   - Book title
   - Price
   - Availability (in stock or not)

4. **Navigation**: Given a Wikipedia page, write a script that:
   - Finds all section headings (h2 tags)
   - Extracts the first paragraph after each heading
   - Creates a summary of the page with headings and their corresponding paragraphs

5. **Advanced**: Create a script that scrapes a news website and:
   - Extracts the top 5 headlines
   - Finds and prints any images associated with these headlines
   - Saves this information to a CSV file

6. **Requests and Error Handling**: Write a script that:
   - Attempts to make a GET request to a user-provided URL
   - Handles common exceptions (e.g., connection errors, timeouts)
   - Prints the status code and headers if the request is successful

7. **API Interaction**: Use the JSONPlaceholder API (https://jsonplaceholder.typicode.com/) to:
   - Fetch a list of users
   - For each user, fetch their todos
   - Print out the name of each user and the number of completed todos they have
