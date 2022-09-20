# Day-52---Intermediate-plus---Instagram-Follower-Bot
# Automated Insternet Speed Checker and Reporting Bot

from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
import time

USR_NME = "your instagram account"
PSSWRD = "your instagram account password"
SIMILAR_ACC = "similar account"
FOLLOWER_COUNT = 5

chrome_driver_path = "D:\Driver\chromedriver.exe"
ser = Service(chrome_driver_path)
driver = webdriver.Chrome(service=ser)


class InstaFollower:
    def __init__(self):
        self.driver = webdriver.Chrome(service=Service(chrome_driver_path))

    def login(self):
        self.driver.get("https://www.instagram.com/accounts/login/")
        time.sleep(4)
        username = self.driver.find_element(By.XPATH, "/html/body/div[1]/section/main/div/div/div[1]/div[2]/form/div/"
                                                      "div[1]/div/label/input")
        username.send_keys(USR_NME)
        password = self.driver.find_element(By.XPATH, "/html/body/div[1]/section/main/div/div/div[1]/div[2]/form/div/"
                                                      "div[2]/div/label/input")
        password.send_keys(PSSWRD)
        password.send_keys(Keys.ENTER)

    def find_followers(self):
        time.sleep(5)
        self.driver.get(f"https://www.instagram.com/{SIMILAR_ACC}/")
        time.sleep(4)
        followers = self.driver.find_element(By.XPATH, "/html/body/div[1]/div/div/div/div[1]/div/div/div/div[1]/div[1]"
                                                       "/section/main/div/header/section/ul/li[2]/a/div/span")
        followers.click()

    def follow(self):
        time.sleep(2)
        for num in range(1, FOLLOWER_COUNT):
            time.sleep(2)
            follow_button = self.driver.find_element(By.XPATH, f"/html/body/div[1]/div/div/div/div[2]/div/div/"
                                                               f"div[1]/div/div[2]/div/div/div/div/div/div/div/"
                                                               f"div[2]/div[1]/div/div[{num}]/div[3]/button")
            if follow_button.text == "Follow":
                follow_button.click()
            else:
                pass


bot = InstaFollower()
bot.login()
bot.find_followers()
bot.follow()
