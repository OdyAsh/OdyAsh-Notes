[source 1](https://www.codementor.io/blog/python-web-scraping-63l2v9sf2q)

# Resolving the Complexities of Web Scraping with Python

## Picking the right tools, libraries, and frameworks

* Native browser tools
* I've found the combination of [Python Requests](http://docs.python-requests.org/en/master/user/quickstart/) (to handle sessions and make HTTP requests) and [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) (for parsing the response and navigating through it to extract info) to be perfect pair.
* For bigger scraping projects (where I have to collect and process a lot of data and deal with non-JS related complexities), [Scrapy](https://scrapy.org/) has been quite useful.
* For JavaScript-heavy sites (or sites that seem too complex), [Selenium](https://www.selenium.dev/) is usually the way to go.

### Handling authentication

* Use  [Python Requests](http://docs.python-requests.org/en/master/user/quickstart/) ,  [Scrapy](https://scrapy.org/), or [Selenium](https://www.selenium.dev/) to maintain cookies and persist our login.
* If there are hidden fields, do the following:
	* Manually login
	* Inspect the payload being sent to the server using the network tools provided by the browser to identify the hidden info being sent.
	* Inspect the headers (e.g., `Authorization`, `Authentication`) sent to the server.
	* Add your findings to the scraping code
		* If the site uses a simple cookie-based authentication, we can also copy the cookie contents and add it to your scraper's code

### Handling Asynchronous loading

#### Detecting Asynchronous loading

* Right-click browser
* Click "view page source"
* Search for the content we're looking for. If you don't find the text in the source, but you're still able to see it in the browser, then it's probably being rendered with JavaScript.
	* Further inspection can be done by checking if there are any XHR request being made by the site.

#### Getting around Asynchronous loading

Options:
* Use web drivers (e.g., Selenium)
* Inspect AJAX calls and try to find requests responsible for fetching the data we're looking for. 
	* We might need to set `X-Requested-With` header to mimic AJAX requests in your script.

To tackle infinite scrolling, here are some options:
* Injecting some JavaScript logic in selenium (see [this SO thread](https://stackoverflow.com/questions/22702277/crawl-site-that-has-infinite-scrolling-using-python)).
* Inspect AJAX calls and implement them in your code.

