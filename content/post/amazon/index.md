---
title: "Find Whole Foods Delivery Slots"
date: 2020-04-08T20:38:10-07:00
draft: false

tags:
- Tutorial
- Life Hack

image:
  caption: Whole Foods Arriving
  focal_point: Smart

---

*I originally posted this tutorial via [Notion](https://www.notion.so/using-pcomputo-s-script-to-find-whole-foods-delivery-slots-acbb6d71ef934da7b6822b1df451a11c?fbclid=IwAR2SeYeXEpI5Q9w92IySz4xeUCfjHyPCe6QBqm8kgd9tztIVXQKcfz74keU).*

Data scientist [Pooja Ahuja](https://github.com/pcomputo) wrote a Python script that automatically sends verbal notification (literally a voice saying "Slots for delivery opened!") as soon as a Whole Foods or an Amazon Fresh delivery slot is open. She offered [detailed instructions](https://github.com/pcomputo/Whole-Foods-Delivery-Slot) for how to use her script. Within 2 seconds of running this script, I found a delivery slot within the next 2 hours. I live in Berkeley so the waiting time may differ for other cities and states...

However, some [Reddit users](https://www.reddit.com/r/amazonprime/comments/frdu50/whole_foods_delivery_slot_finder/) mentioned that as non-coders, they would benefit from this script but didn't know how to. I documented the steps I took so hopefully non-coders and non-Python users can also find delivery slots that they desperately need. **Instructions are specific to macOS and Chrome.**

# Step 0: Install Python 2

You need a Python 2 environment to run the script.

- macOS comes with Python 2.7. To check, go to terminal (search "terminal" in Spotlight → "Terminal" should show up as the first result) and type `python -V` or `python2 -V` (if your default environment is Python 3). If you see something like `python 2.7.11`, then you already have Python 2!
- In case you don't have Python 2, go [here](https://www.python.org/downloads/release/python-273/) and download the version that matches your machine.

# Step 1: Download GitHub repo

- In your terminal, type `cd/PATH` to set your working directory to where you want the GitHub repo to be. For instance, I have a folder dedicated to food so I chose `cd /Users/apple/Desktop/food`.
    - How do you know what to put in the `/PATH` part?
        - Go to Finder → click on "Help" and then search "path" → select "Show Path Bar"
        - Go to your target folder → right click folder name in path bar → copy it as Pathname
        
        {{< figure src="/img/path.png" width="500">}}

- Download the repo: `git clone https://github.com/pcomputo/Whole-Foods-Delivery-Slot`
- Set your working directory to the new folder: `cd Whole-Foods-Delivery-Slot`

# Step 2: Set up ChromeDriver

- Check your Chrome version (to see if it's 79, 80, or 81): click "Chrome" → then "About Google Chrome"

    {{< figure src="/img/chrome.png" width="700">}}

- Go [here](https://chromedriver.chromium.org/) and download a ChromeDriver that matches your Chrome version

- After downloading and unzipping the file, put it in `/usr/local/bin`
    - To find this folder, go to Finder → press Command+Shift+G → enter `/usr/local/bin`
    - After being directed to that folder, put the unzipped "chromedriver" file in there
- To let Python know the path to your ChromeDriver, modify the script that you want to use later
    - Say you want to shop Whole Foods, then open "whole_foods_delivery_slot_chrome.py" 
    - Change `webdriver.Chrome()` to `webdriver.Chrome('/user/local/bin/chromedriver')`

        {{< figure src="/img/chromedriver.png" width="500">}}

    - Save and close the script

# Step 3: Create virtual environment

(Assuming your working directory is still in the "Whole-Foods-Delivery-Slot" folder)

- Type in terminal: `virtualenv -p /usr/bin/python2.7 --distribute temp-python`
- Then: `source temp-python/bin/activate`

# Step 4: Shop Whole Whole Whole

- Go to the [Whole Foods Market](https://www.amazon.com/alm/storefront?almBrandId=VUZHIFdob2xlIEZvb2Rz&ref_=US_TRF_DSK_UFG_WFM_ONSIT_0419987) on Amazon, **not the Whole Foods store on Amazon Prime Now**
- After putting everything you need in the shopping cart, proceed to "Shipping & Payment"

    {{< figure src="/img/stophere.png" width="500">}}

    - If you see a delivery time, then what are you waiting for??!!
    - If no delivery times are available (as they usually are), then use the script to help you.

# Step 5: Run the script

(Make sure you're in the virtual Python 2.7 environment.)

- Install required Python packages by typing in your terminal: `pip install -r requirements.txt`
- Run the script: `python whole_foods_delivery_slot_chrome.py`
- If macOS refuses to open ChromeDriver, go to System Preferences → Security & Privacy to allow it
- If all goes smoothly, the script will open a new Chrome window with an Amazon page like so:

    {{< figure src="/img/success.png" width="700">}}

    - Sign in, proceed to "Shipping & Payment", and stay on that page!
    - Leave the script running, don't close the window, and **turn on your sound (important!!)**
- Go do something else and **wait for a voice saying "Slots for delivery opened!"** (It scared me properly...)
- Upon notification, go back to the window, click on the open slot, and proceed to next steps

**Good luck!**

---

# What about Prime Now?

The author said that the script is intended for the Whole Foods Market on Amazon rather than the Whole Foods store on Amazon Prime Now. But what if we try it on the latter? Here's my attempt:

- Steps 0-3 are exactly the same.
- In step 4, instead of shopping on Amazon proper, shop on Prime Now.
- In step 5, instead of using the Amazon homepage opened by default, go to [Prime Now](https://primenow.amazon.com/).
- Sign-in and proceed to the page below (similar to "Shipping and Payment" on Amazon proper)

    {{< figure src="/img/alt_stop.png" width="500">}}

- The script diligently refreshes the page above, hopefully allowing you to quickly see an open slot.
- Once you see an open slot, click on it and proceed to next steps!
    - **For Prime Now at least, you gotta be quick or the slot may be gone in a few seconds!**

In conclusion, this script is still helpful for Prime Now but I'm not sure if verbal notification works as well.