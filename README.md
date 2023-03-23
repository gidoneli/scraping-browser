# Scraping-Browser

![scraping browser banner](https://github.com/gidoneli/scraping-browser/blob/main/Scraping%20Browser%20(2).jpg)

## Bright Data scraping browser quick start guide

The **Scraping Browser** is a new headful (GUI) automated browser. It was built on top of the Bright Data Web Unlocker infrastructure with the aim of providing a [Puppeteer](https://github.com/puppeteer/puppeteer) or [Playwright](https://github.com/microsoft/playwright-python) compatiable solution for bypassing bot detection on large scale web scraping projects. 

## How to use the Scraping Browser

If you don’t have a verified [Bright Data](https://get.brightdata.com/vitariz8264) account, signing up is free. When your preferred payment method is confirmed you’ll receive a $5 credit to test this tool. Initial rate is $20/GB.

**Step 1:** to create a Scraping Browser zone — go to your Bright Data dashboard, navigate to **‘My Proxies’** page, and under **‘Scraping Browser’** click the **‘Get started’** button.

![Bright Data dashboard screenshot](https://github.com/gidoneli/scraping-browser/blob/main/proxy%20scraping%20browser.png)

**Step 2:** Add a name for your newly created Scraping Browser zone on the **‘Create a new proxy”** page.
Please select a reasonable name for the zone as it cannot be altered once it was created. To create and save your zone, click **'Add proxy'**.

**Step 3:** In order to begin your first Scraping Browser session using **Node.js** or **Python**, here is the initial step for both. Head to your zone’s **‘Access parameters’** tab. There you’ll find API credentials which consist of a Username (Customer_ID), Zone name (attached to username), and Password. This string: ```brd-customer-hl_b685f489-zone-scraping_browser:yq5zs66xnk05``` is an example of what will be required in the following integration scripts.

## Node.js

Install the lightweight Puppeteer-core package (comes without its own browser distribution)

```npm i puppeteer-core```

Simply add your credentials from the **'Access Parameters'** tab - zone, and target URL instead of the placeholders in the below script example.

```const puppeteer = require('puppeteer-core');
const auth = 'brd-customer-hl_b685f489-zone-scraping_browser:yq5zs66xnk05';

async function run(){
    let browser;
    try {
        browser = await puppeteer.connect({
            browserWSEndpoint: `wss://${@zproxy.lum-superproxy.io">auth}@zproxy.lum-superproxy.io:9222`,
        });
        const page = await browser.newPage();
        page.setDefaultNavigationTimeout(2*60*1000);
        await page.goto('http://lumtest.com/myip.json');
        const html = await page
            .evaluate(() => document.documentElement.outerHTML);
        console.log(html);
    } catch(e){
        console.error('run failed', e);
    } finally {
        await browser?.close();
    }
}

if (require.main==module)
    run();
```

Run the script:

```node script.js```
