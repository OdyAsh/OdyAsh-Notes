UpWork Job Requirements To High-Level Python Code
webscraping python tutorial beginners
{%- # TOC start (generated with https://github.com/derlin/bitdowntoc) -%}

- [Introduction](#introduction)
- [Job Requirements](#job-requirements)
- [Understanding The Job Requirements](#understanding-the-job-requirements)
  * [A CSV for Basic Prompt Info](#a-csv-for-basic-prompt-info)
  * [CSVs for Each Prompt's Short Stories](#csvs-for-each-prompts-short-stories)
- [Implementation Outline](#implementation-outline)
- [Code Preliminaries](#code-preliminaries)
  * [Imports](#imports)
  * [Global Variables & Constants](#global-variables-amp-constants)
    + [Navigating Through Reedsy.com](#navigating-through-reedsycom)
    + [Setting the Code's Global Settings](#setting-the-codes-global-settings)
  * [Utility Functions](#utility-functions)
- [Writing High-Level Python Code](#writing-highlevel-python-code)
- [Wrap-Up](#wrapup)

{%- # TOC end -%}

## Introduction

Welcome to the second post in this beginner web-scraping series! :] 🙌

In this post, we'll only cover the task specifications (i.e., UpWork job requirements), the scraping logic, and the high-level Python code, while the next part in this series will delve into the inner workings of each function mentioned in the high-level code.

&nbsp;
## Job Requirements

Upon searching in web-scraping/data-collection tags on [UpWork](https://www.upwork.com/), I found a job listing that had the following requirements:

> Objective Overview: scrape all available information about stories submitted for a specific prompt on Reedsy.

> Task Details: Your task will involve scraping data from Reedsy for stories submitted for a given prompt. The specific information to be collected includes:

> Prompt
Prompt posted date
Number of stories

> The above is one csv file with columns as listed above.

> For each story for a given prompt, collect:

> Prompt - string
Story Title - string
Categories - list
Story text - string
Likes - number
Author - string
Does the story contain sensitive content - binary
Time of Posting (date as well as time) - string
Genre - string
All the comments including 
  the author of the comment, 
  the time of posting of the comment, 
  points of the comment - a 2D list of dictionaries where the key is the author and the value is the comment, with replies having the same structure and belonging to the same internal list

> You will need to visit the Reedsy website, navigate to the prompt's page - https://blog.reedsy.com/creative-writing-prompts/, 
and systematically extract the required information for each story. 
The data should then be organized and saved in separate CSV files for each prompt. 

> The content of each column should be plain text, with HTML content filtered out.

> Deliverables: result files and script in Python


&nbsp;
## Understanding The Job Requirements

From the job description [above](#job-requirements), we can separate what needs to be scraped into two main components:

&nbsp;
### A CSV for Basic Prompt Info

Let's check out the website to see where the prompt info is located:


![finding prompt info location in website](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ovbdr5p56j5n30291uzu.png)

As we can see, we have to click on a prompt to go the page that has the required info, then scrape that info. We do this for each prompt in the chosen genre (e.g., "adventure" as in the image above), then we save all that info in a csv file.

&nbsp;
### CSVs for Each Prompt's Short Stories

Again let's check the website to find the required info for a short story:


![Finding the location of short stories for a chosen prompt](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cyz1h0n62r7cxh5po195.png)

![Top of short story's page](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1vf7yukcl82chs314xkh.png)

![Bottom of short story's page](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pgk342cwzvd36ujwnk5v.png)


So for each prompt, we need to get the URLs for all its short stories, then go to each short story and fetch the required info shown in the images above by the green arrows.

&nbsp;
## Implementation Outline

Here's the outline of `scrape.ipynb` found on [my GitHub repo](https://github.com/OdyAsh/reedsy-prompt-scraping):


![scrape.ipynb outline found created by the notebook's markdown and found at the bottom-left part of VSCode](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8l6h441ql63tfxrslf0j.png)

However, the headers you see above are re-ordered for increased readability of the file, but obviously the [initial versions](https://github.com/OdyAsh/reedsy-prompt-scraping/commits/main) of `scrape.ipynb` weren't as neat as the [current file](https://github.com/OdyAsh/reedsy-prompt-scraping/blob/main/scrape.ipynb). So, in this post, we will talk about each header but in the order shown below:

1. Imports, Global Variables & Utility Functions 
2. Main Code & Visualizing Functions' Return Values
3. Main Functions

Let's get started!

&nbsp;
## Code Preliminaries

Let's take a look at the imports used for this project, global variables/constants, and general utility functions that may be used in this and/or other Python projects.

&nbsp;
### Imports

The following are the imports used along with ChatGPT brief explanation of each package :]:

```python
# built-in packages
import os
import pickle
import time
from pprint import pprint
import re
from datetime import datetime
from typing import List, Dict, Tuple, Union, Optional, Any 

# pip-installed packages
import pandas as pd
import helium as hel
from selenium.webdriver import ChromeOptions
```

![ChatGPT explanation of imports](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/shrqwm9sn9klxf6738cc.png)

Note: High-level decisions like why we chose `helium` library for scraping will be explained at the end of the post.

&nbsp;
### Global Variables & Constants

Let's define global variables as variables that the user might give to the script in order to scrape certain info from the website in a certain way, while constants are values that will most likely not change throughout the scraping code.

&nbsp;
#### Navigating Through [Reedsy.com](https://blog.reedsy.com/creative-writing-prompts/)

Now, we need to first navigate through the website to see what qualifies as variables and what qualifies as constants.

Upon seeing the `creative-writing prompts` page, we see the following:


![reedsy.com top of the page](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h86jchxih3y2d52y922w.png)

![reedsy.com after top of the page](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/n2osf3pxdayzml0baxej.png)

We can notice a couple of things:


1. There are a total of around 2k prompts for all genres (1). However, we're not sure if the client wants all of the prompts or prompts related to a specific genre, so we should make a global variable stating the required genre to scrape (adventure, fiction, etc).

2. If you compare prompt cards at (2), (3), and (4), you'll see that (2) is a live prompt (i.e., there are no saved short stories as the competition is still going), while (3) and (4) are not live prompts. Therefore, we assume the client doesn't mind storing prompts that don't have short stories, and so we'll be taking them into consideration.

3. Another thing, we notice that the base URL is https://blog.reedsy.com/ (1), so we can make this a constant in our code (side-note: eventually, I didn't use this constant anywhere else, but it is good practice to add it along with other constants in case they are used, you can later remove them if they remain unused).

&nbsp;
#### Setting the Code's Global Settings

Given what we described above, here's the import code:

```python
# global variables
GENRE = 'adventure'

# global constants
BASE_URL = "https://blog.reedsy.com/"
options = ChromeOptions()
options.add_argument('--disable-notifications')
options.add_argument('--disable-gpu')
# options.add_argument('--window-size=1280,720')
```


Explanation of `options` constant:

* `ChromeOptions()` is a class in Selenium that allows you to configure various settings and preferences for the Chrome browser.

* we disable the browser's notifications as we want to automate tasks without being interrupted by notification pop-ups.

* Disabling GPU won't usually make a difference in scraping, so this option is just set for laptop battery optimization purposes :].

* Setting the window size might help in some cases where the HTML is easier to parse at a certain [breakpoint](https://www.browserstack.com/guide/responsive-design-breakpoints#:~:text=A%20breakpoint%20in%20a%20responsive,the%20best%20possible%20user%20experience.). This is just for your info, but we won't use this option in our project :].

&nbsp;
### Utility Functions

Throughout your coding journey, you may encounter certain logic that is repeated throughout different projects. It's a good idea to store these logical units as utility functions. In this project, we'll be using the following utility functions:

```python
def save_pkl(content_to_be_saved, path) -> None:
    with open(path, 'wb') as f:
        pickle.dump(content_to_be_saved, f)

def load_pkl(path:str) -> Union[bool, any]:
    if not os.path.exists(path):
        return False
    with open(path, 'rb') as f:
        content = pickle.load(f)
    return content

def join_paths(base_directory:str, relative_path:str) -> str:
    return os.path.normpath(os.path.join(base_directory, relative_path))
```

The function names above gives an indication of their usage. Nevertheless, you can check out [explanations about pickle and path joining](https://chat.openai.com/share/dcce0863-44b3-4205-8b1c-f9da1d1acc69) if you don't know about them. Moreover, you can check the [notebook file](https://github.com/OdyAsh/reedsy-prompt-scraping/blob/main/scrape.ipynb) for extra functions that I have previously coded (but not actually used in this project).


&nbsp;
## Writing High-Level Python Code

The following Python code achieves the logic that we've discussed in the [previous section](#understanding-the-job-requirements):

```python
# start the browser
hel.start_chrome(options=options, headless=False)

# check if prompt_to_short_stories and all_prompts_df are already saved
# from a previous run of the code
prompt_to_short_stories = load_pkl(f'./{GENRE}_prompt_to_short_stories.pkl')
all_prompts_df = load_df_from_csv()

# if either of them is not saved, 
# then we call the functions that scrape and save the data
if prompt_to_short_stories == False or not isinstance(all_prompts_df, pd.DataFrame):
    prompts_urls = get_prompt_urls_by_genre()
    prompt_to_short_stories, all_prompts_df = get_prompt_to_short_stories(prompts_urls)
    save_pkl(prompt_to_short_stories, f'./{GENRE}_prompt_to_short_stories.pkl')
    save_df_to_csv(all_prompts_df)

# scrape and save each of the short stories of each prompt in its own directory
last_short_story_of_last_prompt_df = process_and_save_short_stories_of_each_prompt(prompt_to_short_stories)
```

Notice the lines of code that check if we've already run this code before and saved the output. Even the `process_and_save_short_stories_of_each_prompt()` function internally checks if a prompt's short stories have been previously saved in a CSV. This logic is beneficial when scraping takes time, and you want to instantly save intermediary steps and load them to avoid re-running code to get the same intermediary output.

Side note: for the code block above, you can check the [notebook file](https://github.com/OdyAsh/reedsy-prompt-scraping/blob/main/scrape.ipynb) for code explanations in the form of comments, docstrings, etc.

&nbsp;
## Wrap-Up

In this post of the beginner web-scraping series, we've seen a web-scraping job scenario from UpWork, understood it, navigated through the website to understand its layout, and wrote high-level python code in which its functions will supposedly scrape the Reedsy website in a way that will give us the desired CSVs. Check out the next post in the series to see the logic and implementation of these functions! 🙌