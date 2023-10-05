Using Helium To Scrape Reedsy.com
webscraping python tutorial beginners
{%- # TOC start (generated with https://github.com/derlin/bitdowntoc) -%}

- [Introduction](#introduction)
- [Main Functions](#main-functions)
  * [Save/Load Dataframes to/from CSVs](#saveload-dataframes-tofrom-csvs)
  * [Get Prompts' URLs While Saving To CSV](#get-prompts-urls-while-saving-to-csv)
  * [Map Each Prompt URL To its Stories' URLs](#map-each-prompt-url-to-its-stories-urls)
  * [Save Stories of Each Prompt to CSVs](#save-stories-of-each-prompt-to-csvs)
- [Wrap-Up](#wrapup)
- [Optional: Extra Content](#optional-extra-content)
  * [Understanding Repos Using Bloop.ai & Phind.com](#understanding-repos-using-bloopai-amp-phindcom)

{%- # TOC end -%}

## Introduction

Welcome to the third post in this beginner web-scraping series! :]🙌

Previously, we've seen how to set up our project for a web-scraping project, how to understand a task given from an Upwork job listing, and how to translate the scraping logic into high-level Python code which looked like this:

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

So in this post, we'll thoroughly dive into each of the functions above!

&nbsp;
## Main Functions

Each sub-header will discuss function(s) related to a specific logic from the high-level code.

&nbsp;
### Save/Load Dataframes to/from CSVs

```python
def save_df_to_csv(df:pd.DataFrame, prompt:str=None) -> None:
    # Define the path where you want to save the CSV file
    if prompt:
        output_directory = f'./{sanitize_for_folder_name(GENRE.lower())}/prompts info/'
    else:
        output_directory = f'./{sanitize_for_folder_name(GENRE.lower())}/'

    # Make sure the directory exists; if not, create it
    os.makedirs(output_directory, exist_ok=True)

    # Save the DataFrame to a CSV file in the specified directory
    if prompt:
        output_file = os.path.join(output_directory, f'{sanitize_for_folder_name(prompt)}.csv')
    else:
        output_file = os.path.join(output_directory, f'{GENRE}_all_prompts.csv')

    df.to_csv(output_file, index=False)

def load_df_from_csv(prompt:str=None, return_bool:bool=False) -> Union[bool, pd.DataFrame]:
    # Define the path where you want to load the CSV file from
    if prompt:
        output_directory = f'./{sanitize_for_folder_name(GENRE.lower())}/prompts info/'
    else:
        output_directory = f'./{sanitize_for_folder_name(GENRE.lower())}/'

    # Create the final path for the file that may exist
    if prompt:
        output_file = os.path.join(output_directory, f'{sanitize_for_folder_name(prompt)}.csv')
    else:
        output_file = os.path.join(output_directory, f'all_prompts.csv')

    # Load the DataFrame from the specified CSV file (or return True)
    # Return False if not found
    if os.path.exists(output_file):
        if return_bool:
            return True
        else:
            return pd.read_csv(output_file)
    else:
        return False
```

The functions above assume the following design choices:
- We want to store the CSV of prompt info in a directory with the name of the genre that we've chosen (in our case, "adventure").
  * To accomplish this, we don't pass anything in the `prompt` parameter of the save/load functions.
- Then, we store the CSVs of each prompt in a sub-directory called `prompts info`.

The final output looks like this:


![directory hierarchy of CSVs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ebfhb8mkcx53gfhqiz8t.png)



Of course, there are more than just 3 CSVs in the `prompts info` sub-directory, but I've removed them to make the screenshot easier to see :]

&nbsp;
### Get Prompts' URLs While Saving To CSV

```python
def get_prompt_urls_by_genre():
    prompts_urls = []
    i = 1
    while True:
        # Construct the URL for the current page, go to it, and wait for 0.1 seconds
        url = f"https://blog.reedsy.com/creative-writing-prompts/{GENRE}/page/{i}/"
        hel.go_to(url)
        time.sleep(0.1)

        # Extract all <a> elements that: 
        # 1. contain GENRE string in the value (url) of their href attribute
        # 2. are children of a <div> element with the following classes: 'prompt', 'panel', 'panel-thin', 'panel-white-bordered', 'space-bottom-xs-md'
        a_elements = hel.find_all(hel.S(f'div.prompt.panel.panel-thin.panel-white-bordered.space-bottom-xs-md a[href*="{GENRE}"]'))
        
        # Extract the URLs from the elements and filter by genre
        cur_page_prompts_urls = [url for a_elem in a_elements if GENRE in (url := a_elem.web_element.get_attribute('href'))]
        
        # Break the loop if no more prompts are found
        if len(cur_page_prompts_urls) == 0:
            break
        
        # Extend the list of prompts URLs with the current page's URLs
        prompts_urls.extend(cur_page_prompts_urls)
        
        # Increment the page counter
        i += 1
    
    return prompts_urls
```

Now, the comments above and the ones in the [notebook file](https://github.com/OdyAsh/reedsy-prompt-scraping/blob/main/scrape.ipynb) fairly explain the function above. However, a few subtle points:

1. `time.sleep(1)` is done because sending too many requests (i.e., the `hel.go_to()` lines) will cause the website to not respond to our requests after some time. Note that "1" second was enough as a delay between requests, but you may need to experiment with this value depending on the website that you want to scrape.

2. the CSS selector inside `hel.find_all()` line above fetches `<a>` tags in HTML like this:

    
    ![html of reedsy.com corresponding to the CSS selector in hel.find_all()](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h78xta7xu14du8qdxdk9.png)

    so notice how the classes were separated by '.' in the CSS selector. This is different than separating by a white space, which is done when we want `<a>` tags that are descendants of `<div>` tags.


&nbsp;
### Map Each Prompt URL To its Stories' URLs


```python
def get_prompt_to_short_stories(prompts_urls: List[str]) -> Dict[str, List[str]]:

    prompt_to_short_stories = {}
    parent_csv_col_names = ['prompt', 'prompt posted date', 'number of stories']
    all_prompts_df = pd.DataFrame(columns=parent_csv_col_names)

    for prompt_url in prompts_urls:
        i = 1
        time.sleep(3)
        hel.go_to(f"{prompt_url}?page={i}")

        # Scraping row data for the parent CSV's DataFrame
        prompt = hel.find_all(hel.S("h1.title"))[0].web_element.text

        # "+" means get p element that is the right direct sibling of h1 elements which have "title" class
        # "p:not([class])" means get p element that does not have a class attribute
        uncleaned_prompt_posted_date = hel.find_all(hel.S('h1.title + p:not([class])'))[0].web_element.text
        pattern = r'in (\w+ )+on (\w+ \d+, \d{4})'
        match = re.search(pattern, uncleaned_prompt_posted_date)
        if match:
            prompt_posted_date = match.group(2)
            prompt_posted_date = convert_date(prompt_posted_date)  # Convert date to YYYY-MM-DD format
        else:
            prompt_posted_date = ""

        number_of_stories_text = hel.find_all(hel.S('div.cell h2.mimic-h3'))[0].web_element.text
        match = re.search(r'(\d+) stories', number_of_stories_text)
        
        if match:
            number_of_stories = match.group(1)
        else:
            number_of_stories = 0
        
        # Append the row to the DataFrame
        all_prompts_df.loc[len(all_prompts_df)] = [prompt, prompt_posted_date, number_of_stories]

        # explanation of css selectors used below:
        # get <a> element that is the right direct sibling of <img> elements which have "no-decoration" class
        # and are children of <div> elements which have "submissions-container" id
        submissions_container_a_elements =  hel.find_all(hel.S("#submissions-container img + a.no-decoration"))
        prompt_to_short_stories[prompt] = []

        # Scraping the short stories' URLs of the current prompt_url
        while len(submissions_container_a_elements) > 0:
            short_stories_urls = [elem.web_element.get_attribute('href') for elem in submissions_container_a_elements if 'short-story' in elem.web_element.get_attribute('href')]
            
            prompt_to_short_stories[prompt].extend(short_stories_urls)
            i += 1
            time.sleep(0.3)
            hel.go_to(f"{prompt_url}?page={i}")
            submissions_container_a_elements = hel.find_all(hel.S("#submissions-container img + a.no-decoration"))

    return prompt_to_short_stories, all_prompts_df

```


The function above does two things:

1. gets the `all_prompts_df` data frame which corresponds to this required CSV:


    ![adventure_all_prompts.csv](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/a4aefqk34jcia44cif05.png)


2. returns a dictionary that maps each of the prompts (i.e., the first column in CSV above) to a list of short stories for that prompt:


    ![prompt_to_short_stories dictionary](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3pc5z1p19phv0ra3vh4g.png)

Now, we'll explain a few code snippets from the function above, as the rest can be understood from the comments and the notebook file:

1. `hel.go_to(f"{prompt_url}?page={i}")`:


    ![checking the ?page=1 location in page's url](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b55qxgu9fal1gw3zdqpf.png)

    Side note: when you first visit this page, you won't actually see `?page=1`, so how do we discover it? If we click "Load more stories" at the end of the above page, you will see the new set of short stories appear and the URL will be updated to `?page=2`

2. Regarding this CSS selector `h1.title + p:not([class])`, it will return `<p>` tags in HTML like this:


    ![html related to css selector `h1.title + p:not([class])`](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/se9rfkwpba7t3u1de2t9.png)


3. Regarding the `convert_date()` function, it is a utility function that changes the format of a date string from a date like "Jul 28, 2023" to "2023-07-28". The implementation of this function can be found in the notebook file.

4. Regarding this CSS selector `submissions-container img + a.no-decoration`:


![html related to css selector `submissions-container img + a.no-decoration`](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5s83xykczpoutoe2fsmv.png)


&nbsp;
### Save Stories of Each Prompt to CSVs

```python
def process_and_save_short_stories_of_each_prompt(prompt_to_short_stories: Dict[str, List[str]]) -> None:
    """
    Process and save the short stories (as CSVs) of each prompt in its own directory (which will have the name of the prompt).

    Args:
        prompt_to_short_stories (Dict[str, List[str]]): A dictionary mapping prompts to lists of short story URLs.

    Returns:
        Pandas Dataframe: last short story of last prompt df (to be used for visualization purposes only)

    Example:
        line below will generate folder structure like this:
        ./{GENRE}/prompts info/{prompt_name_of_ith_prompt}.csv
        >>> process_and_save_prompt_data(prompt_to_short_stories)
    """
    children_csvs_col_names = ['prompt', 'story title', 'categories', 'story text', 'likes', 'author', 'story has sensitive content', 'time of posting', 'genre', 'comments']
    short_stories_of_a_prompt_df = None

    for prompt, short_stories in prompt_to_short_stories.items():
        if load_df_from_csv(prompt, return_bool=True):
            continue
        short_stories_of_a_prompt_df = pd.DataFrame(columns=children_csvs_col_names)
        for short_story in short_stories:
            # Going to ith short story
            hel.go_to(short_story)
            time.sleep(0.5)

            # Getting 'story title', 'categories' 'story text', 'likes', 'author', 'story has sensitive content', 'time of posting', 'genre'
            story_title = hel.find_all(hel.S('section.row-blue-dark div.content-thin h1'))[0].web_element.text.strip()
            categories = ", ".join([elem.web_element.text.strip() for elem in hel.find_all(hel.S('p.small.space-top-xs-md a.btn-grey-dark.btn-xxs.btn-rounded.space-right-xs-sm'))])
            story_text = "\n".join([elem.web_element.text.strip() for elem in hel.find_all(hel.S('article.font-alt.submission-content.space-top-xs-md.space-bottom-xs-lg p:not([class]'))])
            likes = hel.find_all(hel.S('p.text-grey.space-top-xs-md > span > button'))[0].web_element.text.split(' likes')[0].strip()
            author = hel.find_all(hel.S('div.grid.no-response.align-middle.gutter-xs-sm a.no-decoration > h4'))[0].web_element.text
            sensitive_content_found = (1 if
                                len(hel.find_all(hel.S('div.panel.panel-thinner.panel-white-bordered.space-bottom-xs-md.space-top-xs-md + article.font-alt.submission-content.space-top-xs-md.space-bottom-xs-lg')))
                                > 0
                                else 0)
            time_of_posting = hel.find_all(hel.S('#submission-report-form + div.cell-shrink'))[0].web_element.text.strip()
            time_of_posting = convert_date(time_of_posting)
            genre = GENRE

            # Getting 'comments'
            comment_threads = []
            parent_comments_containers = hel.find_all(hel.S('#comment-container > div'))
            for parent_comment_container in parent_comments_containers:
                comment_thread = []
                # For a comprehensive list of strategies for find_element(), check this:
                # https://selenium-python.readthedocs.io/locating-elements.html
                comment_thread_elems = parent_comment_container.web_element.find_elements_by_css_selector('div.comment')

                # Getting the parent comment along with all its nested replies as dicts forming a comment_thread list
                for current_comment in comment_thread_elems:
                    c_c_info = current_comment.text.split('\n')
                    c_c_points, c_c_author = c_c_info[0].strip().split(' points ')
                    c_c_date_time = convert_date(c_c_info[1].strip())
                    c_c_comment_text = []
                    for i in range(2, len(c_c_info)):
                        if c_c_info[i].strip() == 'Reply':
                            break
                        c_c_comment_text.append(c_c_info[i])
                    c_c_comment_text = '\n'.join(c_c_comment_text)
                    # # Draft: Use a regular expression to replace consecutive \n with ". "
                    # c_c_comment_text = re.sub(r'\n+', '. ', c_c_comment_text)
                    comment_thread.append({c_c_author: (c_c_date_time, c_c_points, c_c_comment_text)})
                
                # Creating a list of these comment_thread lists
                comment_threads.append(comment_thread)

            short_story_info_row = [prompt, story_title, categories, story_text, likes, author, sensitive_content_found, time_of_posting, genre, comment_threads]
            short_stories_of_a_prompt_df.loc[len(short_stories_of_a_prompt_df)] = short_story_info_row
            
        save_df_to_csv(short_stories_of_a_prompt_df, prompt)
    
    last_short_story_of_last_prompt_df = short_stories_of_a_prompt_df
    return last_short_story_of_last_prompt_df
```

The function above scrapes the required info of each prompt's short stories (visualized [here](#csvs-for-each-prompts-short-stories)), then saves this info in a CSV like this:


![a prompt's CSV of short prompts](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pin9ctgz5hn2wtql4r63.png)


Again, we'll explain a few lines of code in the function above:

1. Regarding the `load_df_from_csv()...`: it checks if the prompt we're currently trying to scrape its short stories' info is already scraped and stored as CSV. If so, move on to the next prompt.

2. The following screenshots visualize the CSS selectors in the following lines respectively: `story_text = ...`, `likes = ...`, `sensitive_content_found = ...`:


    ![story_text CSS selector](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/s3udqcgi9qnluavydlp0.png)

    ![likes CSS selector](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ss3rmjmjk66jxbukzbgz.png)


    ![sensitive_content_found CSS selector](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/aaofscm5vn200thk1an6.png)


3. Regarding the `comment_thread_elems = ...` line, notice how we used `find_elements_by_css_selector()` instead of `hel.S(...)`; this is because we want to **search** for the CSS selector `div.comment` **within a certain scope** of HTML (in our case, the HTML obtained in `parent_comment_container` variable), while `hel.S(...)` will **search **within the page's **entire** HTML. In any case, we can visualize the CSS selector like this:


    ![CSS selector for fetching comments and their replies](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fzwft0kc3s3t0uzy624m.png)


    Recall that we wanted to fetch the content of the comments along with their replies (i.e., nested comments). So, instead of writing recursive code that goes through the nested comments, we obtained their info using `div.comment` CSS selector. Side-note: we probably could've directly obtained them using the `comment-content-xxxxxx` div ids, but the problem is that the last number `xxxxxx` keeps changing, so if you know a way to use helium while fetching HTML's ids with varying suffixes, please inform us in the comment section below :] 🙌.

    Moreover, if you print the `current_comment.text` and `c_c_info` lines by themselves, you get this:


    ![outputting current_comment.text and c_c_info](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4jub3mhqefmdgn8efhog.png)


    Finally, the output of the `comments_threads` variable is like this:


    ![output of comments_threads](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qb17mmnisnuc6mwzceep.png)

&nbsp;
## Wrap-Up

In this series' third entry, we talked in-depth about the functions used to scrape Reedsy.com using `Helium` library (check out the full repo [here](https://github.com/OdyAsh/reedsy-prompt-scraping)), and to be honest, for a "beginners" post, that was **a lot** to take in! But fret not my friend :]☝️, the first step at understanding anything is often the hardest one!

![groundhog day movie meme, it's a doozy](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/krnfld7g8ws95ilqzgzj.gif)

Please inform me of any mistakes or suggestions that you have in the comment section below. I'm also trying to improve my teaching skills, so feel free to comment on how I structure these posts.

I hope you learned a new thing today :]🙌!


&nbsp;
## Optional: Extra Content

Mostly unrelated info that I've learnt along the way and that might come in handy for other projects :]🙌!

Side-note: If you check this post later and find some of these sub-headers removed, then I've probably created a newer post talking specifically about these removed topics.

### Understanding Repos Using Bloop.ai & Phind.com

If you're confused about any of the code snippets above, you can check out [bloop.ai](https://bloop.ai/) and [phind.com](https://www.phind.com/) (along with its [VSCode extension](https://marketplace.visualstudio.com/items?itemName=phind.phind)) to answer any of your questions about the repository, noting that both have free plans.

