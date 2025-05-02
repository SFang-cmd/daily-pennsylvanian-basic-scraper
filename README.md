# Daily Pennsylvanian Headline Scraper

---

## Overview

This project is a Python-based web scraper designed to collect headlines from [The Daily Pennsylvanian](https://www.thedp.com), the University of Pennsylvania's independent student newspaper. The code was adapted from a generic web scraping template and customized specifically for the DP's website structure and ethical guidelines.

**Key Features:**
- Scrapes the most recent/featured news headline as presented in the homepage sidebar.
- Stores daily headline data over time in a JSON file for historical tracking.
- Uses robust CSS selectors tailored for the DP homepage's current layout.
- Built with extensibility and ethical considerations in mind.

---

## How It Works

1. **Fetch the homepage:**  
   The script makes a request to thedailypennsylvanian.com with a desktop browser User-Agent header.

2. **Parse the main sidebar:**  
   Using BeautifulSoup, it locates the sidebar that contains top stories.

3. **Extract the current headline:**  
   The scraper targets the first featured story's headline link and saves its text.

4. **Track and store:**  
   Each day's headline is appended to a JSON file, creating a local archive of DP headlines over time.

---

## Quick Start

1. Clone the repository and install required packages:
    ```bash
    git clone https://github.com/yourusername/dp-headline-scraper.git
    cd dp-headline-scraper
    pip install -r requirements.txt
    ```

2. Run the scraper:
    ```bash
    python script.py
    ```

3. Results will be saved in `data/daily_pennsylvanian_headlines.json` with timestamps.

---

## Customization

- **To scrape other sections (e.g., Sports, Opinion):**  
  Update the CSS selectors in `scrape_data_point()` in `script.py` according to the HTML structure of your target section.
- **To change storage location:**  
  Edit the path provided to the `DailyEventMonitor` class.

---

## Ethical Use and Compliance

- **Respects DP's [robots.txt](https://www.thedp.com/robots.txt):**  
  - Not using a disallowed user agent.
  - Observes crawl-delay (one scrape per day).
- **Intended for personal, educational, or journalistic purposes.**  
  - Do not overload DP's servers or violate their terms of use.
  - Review the [Ethical Guidelines](#some-ethical-guidelines-to-consider) section below.

---

## Part IV Step 4: Modifying the Scraper’s Rule — What Changed?

The original scraper was designed to extract only the main headline from The Daily Pennsylvanian home page. However, the main headline is not always the most interesting or representative story of the day. To make the scraper more flexible and useful, I updated the scraping logic to reliably extract the most recent news article headline from the homepage.

### New Scraping Approach

To accomplish this, the scraper now:

1. **Finds the sidebar containing the top stories**:  
   It searches for the `div` element with the class `top-story-sidebar`, which contains a list of highlighted stories.

2. **Selects the first story in the sidebar**:  
   Within the `top-story-sidebar`, it looks for the first `div` with the class `sidebar-story`. This element represents the most prominent or most recent story featured in the sidebar.

3. **Extracts the headline from the story link**:  
   It then selects the `a` tag with the class `frontpage-link` inside this story, which contains the actual headline text.

By chaining these selectors, the scraper reliably extracts the most recent or featured news article headline as presented in the homepage sidebar.

### Example: Code Logic

The updated logic in the `scrape_data_point()` function follows this pattern (in Python pseudocode):

```python
soup = BeautifulSoup(response.text, "html.parser")
sidebar = soup.select_one("div.top-story-sidebar")
first_story = sidebar.select_one("div.sidebar-story")
headline_link = first_story.select_one("a.frontpage-link")
headline = headline_link.text if headline_link else ""
```

### Why This Change?

- **More relevant headlines:** The sidebar often features timely and topical stories, not just the static or editorial main headline.
- **Greater flexibility:** This structure is less likely to break if the main page layout changes, as the sidebar stories are a consistent feature.
- **Easier extension:** The same approach can be adapted to scrape from other sections (e.g., "Sports", "Opinion", or "Most Read") by tweaking the CSS selectors.

### Next Steps

If you wish to adapt the scraper further (e.g., scrape from other sections like "News", "Sports", "Opinion", or even from other DP publications), you can inspect the HTML structure of your target section and adjust the selectors in the `scrape_data_point()` function accordingly.

---

## Licensing

This software is distributed under the terms of the MIT License. You have the freedom to use, modify, distribute, and sell it for any purpose. However, you must include the original copyright notice and the permission notice found in the LICENSE file in all copies or substantial portions of the software.

You can [read more about the MIT license](https://choosealicense.com/licenses/mit/), and [compare different open-source licenses at `choosealicense.com`](https://choosealicense.com/licenses/).

## Some Ethical Guidelines to Consider

Web scraping is a powerful tool for gathering data, and its [legality has been upheld](https://en.wikipedia.org/wiki/HiQ_Labs_v._LinkedIn).

But it is important to use it responsibly and ethically. Here are some guidelines to consider:

1. Review the website's Terms of Service and [`robots.txt`](https://en.wikipedia.org/wiki/robots.txt) file to understand allowances and restrictions for automated scraping before starting.

2. Avoid scraping copyrighted content verbatim without permission. Summarizing is safer. Use data judiciously under "fair use" principles.

3. Do not enable illegal or fraudulent uses of scraped data, and be mindful of security and privacy.

4. Check that your scraping activity does not overload or harm the website's servers. Scale activity gradually.

5. Reflect on whether scraping could unintentionally reveal private user or organizational information from the site.

6. Consider if scraped data could negatively impact the website's value or business model.

7. Assess if decisions made using the data could contribute to bias, discrimination or unfair profiling.

8. Validate quality of scraped data, and recognize limitations in ensuring relevance and accuracy inherent with web data.  

9. Document your scraping process thoroughly for replicability, transparency and accountability.

10. Continuously re-evaluate your scraping program against applicable laws and ethical principles.
