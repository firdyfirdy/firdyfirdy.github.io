---
title: "Unlocking the Gate: A Guide to Bypassing Cloudflare Turnstile CAPTCHA"
date: 2024-10-05 19:36:00 +07000
categories: [bypass captcha, scraping, web scraping]
tags: [bypass captcha, scraping, web scraping]
---

When scraping a web application, we almost always face an anti-bot, the nemesis of web scrapers, which is Captcha. For those who don't know what Captcha is, Captcha is a test used on websites to make sure you're a human, not a robot. It usually asks you to solve simple challenges like clicking on pictures, typing words, or checking a box that says, "I'm not a robot."<br>
There are so many types of Captcha on the internet, such as Google’s reCAPTCHA, or the one we will discuss today, Cloudflare Turnstile.<br>
Usually, to bypass a Captcha, we need a third party, which often comes with a certain fee. However, in this article, I will share how to bypass Cloudflare Turnstile without paying for third-party services.<br>
Let me introduce the tool, which is [Puppeteer Real Browser](https://github.com/zfcsoftware/puppeteer-real-browser).<br>
For web scrapers, the term Puppeteer is probably familiar; to give an overview, Puppeteer is a JavaScript library that provides a high-level API to control Chrome or Firefox over the DevTools Protocol or WebDriver BiDi.<br>
With the help of the Puppeteer Real Browser tool, we can perform scraping without worrying about how to bypass Cloudflare's Captcha.<br>
For more detailed information, you can visit the official GitHub page [Puppeteer Real Browser](https://github.com/zfcsoftware/puppeteer-real-browser).
<br>
## Installation
```bash
npm i puppeteer-real-browser
```

If you are using a Linux operating system, xvfb must be installed for the library to work correctly.<br>
```bash
sudo apt-get install xvfb
```

## Usage
``` js

const { connect } = require("puppeteer-real-browser")

async function test() {
    const { browser, page } = await connect({
        headless: false,
        args: [],
        customConfig: {},
        turnstile: true,
        connectOption: {},
        disableXvfb: false,
        ignoreAllFlags: false
    })
    await page.goto('<url>')
}

test()
```

## Example
Here is a video of a comparison between Puppeteer and Puppeteer Real Browser:

### Using Puppeteer
{% include embed/video.html src='https://github.com/user-attachments/assets/dcb53256-3aa8-4791-9b85-098e9aac132c' %}

### Using Puppeteer Real Browser
{% include embed/video.html src='https://github.com/user-attachments/assets/fddef29c-9dbe-4af0-860b-295ef939798f' %}
