# ao3
Browser automation with Selenium


# Importing the packages 
import selenium
from selenium import webdriver
from selenium.webdriver.support.ui import Select
import time


# Opening the browser

PATH = "C:\Program Files (x86)\chromedriver.exe"
driver = webdriver.Chrome(PATH)

# Accessing the site
driver.get('https://archiveofourown.org/')


# Agreeing to the terms 
agree = driver.find_element_by_id('tos_agree')
agree.click()
button = driver.find_element_by_name('button')
button.click()

time.sleep(5)

# Selecting the type of media you want 
choice = input("What fandom you're looking for?\n\n Choose Books, Celebrities, Bands, Theater, Video Games, Anime, Cartoons, Movies or TV Shows")

fandom = driver.find_element_by_partial_link_text(choice.capitalize())
fandom.click()


# Selecting the fandom you want
question = input("What media are you looking for?")

media = driver.find_element_by_partial_link_text(question.title())
media.click()

time.sleep(5)

# Selecting the Order filter
kudos = Select(driver.find_element_by_id('work_search_sort_column'))
kudos.select_by_visible_text('Kudos')


# Opening the toggle menu for completition
other_button = driver.find_element_by_id('toggle_work_complete')
other_button.click()


# Chosing the kind of work you want, here we're choosing only completed works
complete = driver.find_element_by_xpath('//input[@id="work_search_complete_t"]')
driver.execute_script("arguments[0].click();", complete)

# Clicking the buttom to commit all this filters
commit = driver.find_element_by_xpath("//input[@value='Sort and Filter']")
commit.click()

time.sleep(5)


# Getting the info on the first 5 fics
li = driver.find_elements_by_xpath("//li[@role='article']")
works = 5

for l in range(works):
    print(li[l % len(li)].text, '\n\n')
