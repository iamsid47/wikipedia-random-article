---
name: 'Wikipedia Random Article Suggestion'
description: 'This program scrapes wikipedia and suggests a random article for the user to read.'
author: '@iamsid47'
img: https://github.com/iamsid47/hangman-pics/blob/main/hangman.png
---

Hi there! In this workshop we are gonna build a Wikipedia Article Recommender/Suggester. This program is built using Python and works well on an online IDE or locally.

You can try out this program on Repl.it using [THIS](https://repl.it/@iamsid47/wikipedia-scraper#main.py) link.

## Files & Libraries

This program will consist of just one python file named as `main.py`. There are a couple of libraries required such as `bs4`, `requests`, and `random`.

## Let's Get Started

First, let's head over to [Repl.it](https://repl.it) and create a *repl*. Choose the language as Python and name your project.

Next, let's install the required libraries and later import them.

First, we will install `beautifulsoup4` aka `bs4`. So, head over to the shell and type in: `pip install bs4`. Now let us import the libraries to our  `main.py` file.

```python
import requests
from bs4 import BeautifulSoup
import random
```

So basically all the libraries are used in some or the other way. The `requests` library is for getting requests (http/https). The `bs4` library is used for scraping and the `random` library will be used for random article selection.

Now let's use `requests` and define a variable named **`response`**.

```python
response = requests.get(
	url="https://en.wikipedia.org/wiki/Web_scraping",
)
```

Here, I have used Wikipedia's web_scraping page for our requests.

Next, we will call `bs4` to parse the HTML for us and store it into a variable named **`soup`**.

```python
soup = BeautifulSoup(response.content, 'html.parser')
```

Now we have all the content of the page inside the variable named `soup`. After this, we will capture the **Title** of the web page from the data we have stored in `soup`. For this purpose need to know that what type of tags and classes has Wikipedia used to define it's HTML pages.

So, let's head over to a Wikipedia article. I just found the *How to write a Wikipedia article page*, so I'll use the same. Note that the `h1` tag in all the pages of Wikipedia is the same. Thus, there will not be any difference.

Here we can see that they use the *id*: `firstHeading` to define their titles. So, we will use this id to get the titile from `soup` as it will also be the same. Next, we print this titile.

```python
title = soup.find(id="firstHeading")
print(title.content)
```

Now this is an article scraper which will scrape URLs and list any one of those as a recommendation. Thus, we don't want other parts of the page from `soup` to get listed.
Hence, we will seperate the links from `soup` and then keep them in another variable named `allLinks`.

After this, we want to select just one link from these links but that shall be random. So, first we shuffle all the links and then create an empty variable named `linkToScrape`.

```python
allLinks = soup.find(id="bodyContent").find_all("a")
random.shuffle(allLinks)
linkToScrape = 0
```

Next, we are only interested in the links that direct us to some other article and not anything which is on-the-current page. So, we will exclude the on-page links.

```python
for link in allLinks:
	if link['href'].find("/wiki/") == -1: 
	continue
```

Now, we use those links to scrape the page. For this purpose, we make:

```python
linkToScrape = link
	break
```

and then break this operation as we don't want other links.

Lastly, we print the link we just scraped.

```python
print(linkToScrape)
```

## Voila!

You just made your very own Wikipedia Article Scraper!

## Hack It ;)

Furthermore, there are a ton of ideas for this. You can make a scraper which will not only scrape one link, but many of them at the same time. You can also make a scraper which fetches the whole article and throws the output on the command-line. But you shall be able to exclude the tags as well, because `bs4` takes the whole page with the code as well.

You can also make a scraper which suggests just the heading of Wikipedia and then you can have a search for that article.

There is also a possibility where you can scrape other websites instead of just Wikipedia! A great example would be to scrape Medium or Reddit.
