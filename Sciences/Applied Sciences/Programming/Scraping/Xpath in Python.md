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
	* "//" --> starting from the `browser`'s root
* `divElement.find_element_by_xpath(".//child::p")` 
	* "element" -->gets first direct child 
	* "::p" --> with the  `<p>`  tag starting 
	* ".//" --> from the div element specified by the object `divElement`
# first vs last element
* `divElement.find_element_by_xpath(".//child::p[1]")` gets first child element of `divElement` with `<p>` tag
* `divElement.find_element_by_xpath("(.//child::p)[last()]")` gets first child element of `divElement` with `<p>` tag [source](https://stackoverflow.com/questions/1459132/xslt-getting-last-element#:~:text=indexing%20on%20the%20nodelist%20result%2C%20rather%20than%20as%20part%20of%20the%20selection%20criteria.%20Try%3A)
