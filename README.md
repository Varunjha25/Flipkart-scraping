# Flipkart-scraping
![Uploading image.png…]()

Web Scraping with Selenium and Saving Data to SQLite Database
clear and reflects the main purpose of the code: using Selenium to scrape data and storing it in an SQLite database
Breaking down the code 
Import SQLite3
Form selenium  import webdriver
From selenium.webdriver.chrome.service import service
From selenium.webdriver.chrome.by import by
From selenium.webdriver.chrome.option import option
What is happening here ?
We are bringing tools in different jobs
•	SQLite3 : A tool for taking to a small database where we will save data 
•	Selenium : A tools that helps us control a browser like a robot
•	Other parts like( Service, By, Option) are like helpers that make selenium works better
Configure ChromeDriver Path and User Agent

chrome_driver_path = r"C:\Users\Ankit\Downloads\chromedriver-win64\chromedriver-win64\chromedriver.exe"
user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36"
What is happening here ?
•	We tell the program where to find  the chrome driver (a spls tools that helps control google chrome)
•	User_agent is like a fake identify card that’s tell the website, “Hey I am just a normal person using browser”
Setup Chrome Options

Chrome_options = Options()
Chrome_options.add_argument(f”user-agent={user-agent}”)
Chrome_options.add_argument(“—headless”)
Chrome_option.add_arguments(“—disable-gpu”)
Chrome_option.add_arguments(“—no-sandbox”)

What is happing here?
We are giving special instruction to chrome:
•	Pretend to be normal user(with the user_agent)
•	Work silently in the background(-- headless), no browser window will pop up
•	Don’t use graphics power(--disable-gpu)
•	Ignore some unnecessary security checks(--no-sandbox)
Start the Browser

Service = service (chrome_driver_path)
Driver = webdriver.chrome(service = service,  options = chrome_options)

What is happing here ?
We are saying
•	“Use the chromeDriver tool to open chrome”
•	Follow the special rule(options) we are just setup

Set Up the Database

Db_name = “scraped_data.db”

Table_name =”scraped_links” 

Conn = sqlite3.connect(db_name)
Cursor =  conn.cursor()

What is happing here ?

•	Scrapped_data.db  is small file where we save our data

•	Cursor is like pen that write commands to the database

Create the Table
cursor.execute(f"""
CREATE TABLE IF NOT EXISTS {table_name} (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT,
    link TEXT
)
""")
conn.commit()

What is happening here ?
•	We tell  the database to create table name scraped_links
•	The table have three columns
•	Id : unique number of each row
•	Title : the text form website links
•	Links :  the url of the links
•	If not exists means,  “ Don’t create the if already there

Open the Website and Scrape Data
url = https://www.flipkart.com/
try: 
    driver.get(url)
    elements = driver.find.elements(By.css_selector, “a”)
   scraped_data  = [{“title”: e.text, “links”: e.get_attribute(“href”)} for e in elements if e.text.strip()]

What is happening here ?
•	Go to the website : the browser opens https://www.flipkart.com/
•	Find all links : its look for <a>  tag on the web page(these tags represent links
 
Save usefull info :for each link
•  title is the text of the link.
