# Mission-to-Mars

## Purpose of the web page
In this challenge, I am scraping web data to create a web page with facts, images and recent news on Mars for a client who is wanting to impress NASA. We created a web app with Flask, html files and MonoDB. 

In order to create the python file to scrape the data we wanted for our web app, we used the following tools:
- BeautifulSoup
- Splinter
- Pandas
- ChromeDriverManager

## Challenge
For this challenge in particular, we scraped the four Mars images and their corresponding titles from https://marshemispheres.com/. In order to do this, I first had to locate each images href in a for loop, click on each one and scrape the image URL and title. 

The code I used to perform this action:
```
url = 'https://marshemispheres.com/'
browser.visit(url)
html = browser.html
hem_soup = soup(html, 'html.parser')

hemisphere_image_urls = []

href = hem_soup.find_all('div', class_='item')

for e in list(href):
    hemispheres = {}
    
    link = e.find("a")['href']
    browser.visit(url + link)
    html = browser.html
    hem_soup = soup(html, 'html.parser')
    
    img_url_rel = hem_soup.find('li').find("a")['href']
    title = hem_soup.find('h2', class_="title").get_text()
    img_url = f'https://marshemispheres.com/{img_url_rel}'

    hemispheres['image_url'] = img_url
    hemispheres['title'] = title
    
    browser.back()
    hemisphere_image_urls.append(hemispheres)
 ```
Once I got my code to perform in Jupyter Notebook, I was able to download it as a python file and copy over the code into my scraping.py file. In order for my Flask app to work and talk to the scraping.py file and index.html file, I had to do the following:
- Create a function for the mars hemisphere images
- Make sure it aligns with the html file and code

Everything worked great and I then updated the html to work for mobile.

