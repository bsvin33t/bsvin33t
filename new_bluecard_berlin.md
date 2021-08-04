### Blue card check.

Recently I wanted to renew my bluecard. Being a resident of Berlin, it is near impossible to get an appointment at any point of the day. 
Which is why, in tandem with `checklyhq`(a neat little site to do regression testing on your web applications), I wrote myself a tiny script which checks for appointments every 5 minutes.
And voilà, I was able to find an appointment the next day and I even submitted my documents yesterday(3rd).

Here is the `playwright` script(sure there's better way to do this, but whaterver. I already spent half hour doing this, I didn't want to spend any time more):

```
const { chromium } = require("playwright")
const expect = require("expect")

// Start a browser session
const browser = await chromium.launch()
const page = await browser.newPage()

// Go to a page. This waits till the 'load' event by default
await page.goto(
  "https://otv.verwalt-berlin.de/ams/TerminBuchen/wizardng/9d68ff8e-90b4-44f2-ac21-93fdb92ad907?dswid=2534&dsrid=745&st=2&v=1626937415358"
)
await page.waitForTimeout(30000)
// Assert a specific page item to be present
await page.click('button[role="button"]:has-text("Weiter")')
await page.waitForTimeout(40000)
// Snap a screenshot
await page.screenshot({ path: "screen.png", fullScreen: true })
const received = await page.$eval(
  ".errorMessage",
  (el) => el.textContent.toString()
)
console.log("*******")
console.log(received)
console.log("*******")

const expected = "Für die gewählte Dienstleistung sind aktuell keine Termine frei! Bitte versuchen Sie es zu einem späteren Zeitpunkt erneut.".split("")
const totalLength = received.split("").filter(n => !expected.includes(n)).length

expect(totalLength).toBeLessThan(5);

// Close the session
await browser.close()
```
