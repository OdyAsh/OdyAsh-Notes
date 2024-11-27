Examples are mostly found in `bue_scraper.ipynb` [here](https://github.com/OdyAsh/bue-scrapper)
# Xpath Cheatsheet
[source](https://devhints.io/xpath)
![](Attachments%20-%20Xpath%20in%20Python/Pasted%20image%2020230209183846.png)
* div p vs div > p ([source](https://teamtreehouse.com/community/is-there-a-difference-between-div-p-and-div-p#:~:text=%5Bdiv%20%3E%20p%5D%20selects%20only,a%20div%20would%20be%20affected.)):
	* [div > p] (i.e., //div/p in xpath) selects only the p that are **children** of the div. So if you had a div with lists or whatever inside that had their own p, their properties would not be affected by this selector.
	* [div p] (i.e., //div//p in xpath) selects all **descendant** p in the div. So any p that is inside, or descendant, of a div would be affected.
![](Attachments%20-%20Xpath%20in%20Python/Pasted%20image%2020230209184311.png)
![](Attachments%20-%20Xpath%20in%20Python/Pasted%20image%2020230209184412.png)

# // vs .//
* `divElement.find_elements_by_xpath("//descendant::a")` 
	* "element**s**" --> gets all descendants (i.e., child, grandchild, etc) 
	* "::a" --> with the  `<a>`  tag 
	* "//" --> <mark style="background: #D2B3FFA6;">starting from</mark> the `browser`'s <mark style="background: #D2B3FFA6;">root</mark>
* `divElement.find_element_by_xpath(".//child::p")` 
	* "element" -->gets first direct child 
	* "::p" --> with the  `<p>`  tag 
	* ".//" --> <mark style="background: #D2B3FFA6;">starting from the div element</mark> specified by the object `divElement`
# first vs last element
* `divElement.find_element_by_xpath(".//child::p[1]")` gets first child element of `divElement` with `<p>` tag
* `divElement.find_element_by_xpath("(.//child::p)[last()]")` gets last child element of `divElement` with `<p>` tag [source](https://stackoverflow.com/questions/1459132/xslt-getting-last-element#:~:text=indexing%20on%20the%20nodelist%20result%2C%20rather%20than%20as%20part%20of%20the%20selection%20criteria.%20Try%3A)

# text() vs "." (or string()) vs contains()

Suppose that currently, the driver's `page_source` contains the following (notice the whitespace in " Submit"):
```html
<button class="lg primary svelte-cmf5ev" id="component-14"> Submit</button>
```
Then:
```python
# doesn't work in xpath 1.0 (which is the default for all browsers as of 2024)
# Note for the future: this is a way to check if the browser is using xpath 2.0 or 1.0
driver.find_element(By.XPATH, "//button[ends-with(@id, '33')]").get_attribute("outerHTML")

# text() + ' Submit' doesn't work, 
# as per xpath 1.0's specifications: 
#   text() divides the string into multiple nodes, 
#   therefore the comparison by exactly matching either ' ' or 'Submit', 
#   but not a concatentation of both (i.e., ' Submit) (I think)
driver.find_element(By.XPATH, "//button[text()=' Submit']").get_attribute("outerHTML")

# text() + 'Submit' works
# as it matches one of the text()'s returned node: "Submit"
driver.find_element(By.XPATH, "//button[text()='Submit']").get_attribute("outerHTML")

# this is also why text() + ' ' works 
elements_2 = driver.find_elements(By.XPATH, "//button[text()=' ']")
for element in elements_2:
    # side note: element.text returns the trimmed text visible on the page, 
    # while element.get_attribute("textContent") returns the full raw text inside the element 
    if element.get_attribute("textContent") == " Submit":
        print(element.get_attribute("outerHTML"))

# '.'/string() + ' Submit' works
driver.find_element(By.XPATH, "//button[.=' Submit']").get_attribute("outerHTML") # "." same as "string()"

# '.'/string() + 'Submit' doesn't work, as "=" means exact matching
driver.find_element(By.XPATH, "//button[.='Submit']").get_attribute("outerHTML")

# contains() + '.'/string() + ' Submit'/'Submit' works (preferred method)
elements_2 = driver.find_elements(By.XPATH, "//button[contains(., 'Submit')]")
for element in elements_2:
    print(element.get_attribute("outerHTML"))
```

Finally, in all of the above cases, the matching is case-sensitive.

Relevant links:
* Browsers supporting only xpath 1.0 as of 2024: https://stackoverflow.com/questions/25455351/does-chrome-use-xpath-2-0
* dot (".") vs text() (important): 
	* https://stackoverflow.com/questions/34593753/testing-text-nodes-vs-string-values-in-xpath
	* https://stackoverflow.com/questions/38240763/xpath-difference-between-dot-and-text
* string() vs text(): https://stackoverflow.com/questions/9493732/difference-between-text-and-string?rq=3
* ends-with() working in xpath 2.0 only: https://stackoverflow.com/a/40935676/13626137
* text node in the DOM tree: https://developer.mozilla.org/en-US/docs/Web/API/Text
* contains(): https://www.roborabbit.com/blog/everything-you-need-to-know-about-the-xpath-contains-function/#xpath-vs-css-selectors-which-one-to-use