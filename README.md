# BookScrape_web
Scrape book data from the website Books to Scrape and store the information in a structured format
Web Scraping Task: Books to Scrape


Objective:
The goal of this task is to scrape book data from the website Books to Scrape and store the information in a structured format (CSV or JSON).



Task Breakdown:
Data to Scrape: From each book listed on the website, scrape the following information:
Book Title: The title of the book.
Price: The price of the book.
Availability: Whether the book is in stock or out of stock.
Rating: The star rating of the book (e.g., 3 stars, 5 stars, etc.).
Book URL: The URL of the detailed book page.
Book Image URL


Pagination: The website contains multiple pages of books. You will need to scrape all books by:
Iterating through each page and collecting the above information for all books.


Final Output: Save the scraped data in a structured format:


CSV: Save as books_data.csv, with columns for Title, Price, Availability, Rating, and Book URL.
Alternatively, you can use JSON if you prefer. Ensure the file is well-structured.



Here's an explanation of each part of the code:

1. get_doc(url) function:
This function sends an HTTP GET request to a URL and parses the response into a BeautifulSoup object for further processing.

requests.get(url): Sends an HTTP request to the given URL and returns the response.
BeautifulSoup(response.text, 'html.parser'): Parses the HTML content of the webpage using BeautifulSoup, making it easier to extract specific data.
if response.status_code != 200: Checks if the request was successful (status code 200). If not, it raises an exception.
Returns: The parsed HTML document.



2. scrape_multiple_pages(n) function:
This function scrapes data from multiple pages of the Books to Scrape website, gathering book titles, prices, availability, ratings, URLs, and image URLs. It creates a DataFrame containing this information for further use.

Parameters:
n: The number of pages to scrape.


Steps:
Initial setup:
URL = 'https://books.toscrape.com/catalogue/page-': Base URL for the website, which will be appended with page numbers.
Lists are created for storing the scraped data: b_title, b_price, b_stock, b_rating, b_url, and b_imgurl.
Loop through the pages:
for page in range(1, n+1): Loops through each page (from page 1 to n).
get_doc(URL + str(page)+ '.html'): Calls get_doc() to retrieve the HTML document for each page by appending the page number to the base URL.
Extracting book data:
Each page’s HTML content is processed using helper functions (not shown in the provided code):

get_book_titles(doc): Extracts the book titles.
get_Book_price(doc): Extracts the book prices.
get_book_availability(doc): Extracts whether the book is in stock or not.
get_book_rating(doc): Extracts the book ratings.
get_book_url(doc): Extracts the URL of the book.
get_image_url(doc): Extracts the URL of the book’s image.
For each page, these extracted pieces of information are appended to the corresponding lists (b_title, b_price, etc.).

Storing data in a dictionary:
book_dict1: A dictionary is created, where each key (e.g., 'TITLE') corresponds to a list of the extracted data.
Returning a DataFrame:
pd.DataFrame(book_dict1): Converts the dictionary into a pandas DataFrame, where each key becomes a column, and the values (lists) become the rows of the DataFrame.
