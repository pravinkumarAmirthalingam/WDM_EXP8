### EX8 Web Scraping On E-commerce platform using BeautifulSoup
### DATE: 27-08-26
### AIM: To perform Web Scraping on Amazon using (beautifulsoup) Python.
### Description: 
<div align = "justify">
Web scraping is the process of extracting data from various websites and parsing it. In other words, it’s a technique 
to extract unstructured data and store that data either in a local file or in a database. 
There are many ways to collect data that involve a huge amount of hard work and consume a lot of time. Web scraping can save programmers many hours. Beautiful Soup is a Python web scraping library that allows us to parse and scrape HTML and XML pages. 
One can search, navigate, and modify data using a parser. It’s versatile and saves a lot of time.
<p>The basic steps involved in web scraping are:
<p>1) Loading the document (HTML content)
<p>2) Parsing the document
<p>3) Extraction
<p>4) Transformation

### Procedure:

1) Import necessary libraries (requests, BeautifulSoup, re, matplotlib.pyplot).
2) Define convert_price_to_float(price) Function: to Remove non-numeric characters from a price string and convert it to a float.
3) Define get_amazon_products(search_query) Function: to Scrape Amazon for product information based on the search query.
4) Fetch and parse the HTML content then Extract product names and prices from the search results and Sort product information based on converted prices in ascending order.
5) Return sorted product data as a list of dictionaries.
6) Call get_amazon_products(search_query) to get product data based on the user's search query.
7) Check if products are found; if not, display "No products found."
8) Visualize Product Data using a Bar Chart

### Program:
```
from bs4 import BeautifulSoup
import time
import requests
import matplotlib.pyplot as plt

query = input("Enter the query to search: ").lower().strip()
pages = int(input("Enter number of pages to traverse: "))
base_url = "https://webscraper.io/test-sites/e-commerce/static/computers/laptops?page="
found = []

for page in range(1, pages + 1):
    url = base_url + str(page)
    print(f"\nChecking Page {page}...")
    response = requests.get(url)
    if response.status_code == 200:
        soup = BeautifulSoup(response.text, "html.parser")
        product = soup.find_all("div", class_="thumbnail")
        for i in product:
            title = i.find("a", class_="title").text.strip().lower()
            if query in title:
                price = i.find("h4", class_="price").text.strip()
                desc = i.find("p", class_="description").text.strip()
                rating = i.find("p", {"data-rating": True})["data-rating"]
                review = i.find("span", itemprop="reviewCount").text.strip()
                found.append({"title": title,"price": price,"desc": desc,"rating": rating,"review": review})
        time.sleep(1)
    else:
        print("Failed to load page:", page)

print("\nResults Found:", len(found))
print()
j = 1
for ii in found:
    print("Product:", j)
    j += 1
    print("Title :", ii["title"])
    print("Price :", ii["price"])
    print("Desc :", ii["desc"])
    print("Rating :", ii["rating"])
    print("Review :", ii["review"])
    print()

if found:
    product_names = []
    product_prices = []
    for item in found:
        product_names.append(item["title"])
        product_prices.append(float(item["price"].replace("$","")))
    plt.figure(figsize=(12,8))
    plt.bar(product_names, product_prices)
    plt.xlabel("Product Name")
    plt.ylabel("Price ($)")
    plt.title("Laptop Prices from Web Scraping")
    plt.tight_layout()
    plt.show()
else:
    print("No products found to plot")


```

### Output:

<img width="639" height="934" alt="Screenshot 2026-08-17 110956" src="https://github.com/user-attachments/assets/8c19f32a-c7f2-4892-9ac7-b436b4170b26" />

<img width="1047" height="717" alt="Screenshot 2026-08-17 111016" src="https://github.com/user-attachments/assets/b2bb3cdb-8e3b-4c4c-bedc-2de2fc454e28" />

### Result:
Thus, We had Successfully implemented the Web Scraping on a E-commerce platform using (beautifulsoup) Python.



