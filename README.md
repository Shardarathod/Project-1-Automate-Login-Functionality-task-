# Project-1-Automate-Login-Functionality-task-
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
import time

# Setup Chrome driver
driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))

# Maximize window
driver.maximize_window()

# Open website
driver.get("https://the-internet.herokuapp.com/login")

# Wait for page to load
time.sleep(2)

# Locate elements
username = driver.find_element(By.ID, "username")
password = driver.find_element(By.ID, "password")
login_button = driver.find_element(By.XPATH, "//button[@type='submit']")

# Enter credentials
username.send_keys("tomsmith")
password.send_keys("SuperSecretPassword!")

# Click login
login_button.click()

# Wait for result
time.sleep(2)

# Verify login success
message = driver.find_element(By.ID, "flash").text

if "You logged into a secure area!" in message:
    print("✅ Login Successful")
else:
    print("❌ Login Failed")

# Close browser
driver.quit()
