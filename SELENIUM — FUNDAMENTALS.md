SELENIUM — FUNDAMENTALS
191. What is Selenium?
🎯 Interview Answer

Selenium is an open-source automation framework used to automate web applications across different browsers and operating systems.

It supports multiple programming languages such as Java, Python, C#, and JavaScript/TypeScript.

In my projects, I mainly use Selenium WebDriver with Java to automate web UI test cases such as login, form submission, validations, tables, windows, alerts, and end-to-end business workflows.

⭐ Important

Selenium is primarily for web application automation. It is not designed for desktop application automation.

192. What are the components of Selenium?

Selenium mainly consists of:

Selenium WebDriver
Selenium IDE
Selenium Grid
1. WebDriver

Used for programmatically automating web browsers.

2. Selenium IDE

A browser-based record-and-playback tool mainly useful for creating quick automation scripts/prototypes.

3. Selenium Grid

Used to execute tests across multiple browsers, machines, and environments, supporting parallel execution.

🎯 Interview Answer

"The main Selenium components are WebDriver, IDE and Grid. WebDriver is used for browser automation, IDE is mainly used for record-and-playback, and Grid is used for distributed and parallel execution across different browsers and machines."

193. What is Selenium WebDriver?
🎯 Interview Answer

Selenium WebDriver is an API that allows us to automate and control web browsers programmatically.

For example, with Java + Selenium WebDriver, I can:

Open a browser
Navigate to a URL
Find elements
Enter text
Click buttons
Handle dropdowns
Handle alerts
Switch windows/tabs
Take screenshots
Execute JavaScript
Validate web application behavior
Example
WebDriver driver = new ChromeDriver();

driver.get("https://example.com");

driver.findElement(By.id("username"))
      .sendKeys("admin");

driver.findElement(By.id("login"))
      .click();
194. What is Selenium IDE?
🎯 Interview Answer

Selenium IDE is a browser extension/tool that provides record-and-playback functionality for web automation.

It allows us to record user interactions and replay them.

It is useful for:

Quick prototypes
Simple automation
Learning Selenium concepts
Creating quick reproduction scripts

However, for a large enterprise automation framework, I would generally use WebDriver with Java and TestNG/JUnit rather than depending on IDE.

195. What is Selenium Grid?
🎯 Interview Answer

Selenium Grid allows Selenium tests to run on different machines, browsers, and operating systems, and supports parallel execution.

For example, suppose I have 100 test cases.

Instead of:

Machine 1
Chrome → 100 tests sequentially

I can distribute them:

Machine 1 → Chrome
Machine 2 → Firefox
Machine 3 → Edge

This can significantly reduce execution time.

Real-time example

If regression takes:

Chrome → 2 hours

I can distribute tests across multiple browser nodes and execute them in parallel.

⭐ Interview point

"Grid is especially useful when cross-browser and parallel execution is required."

196. Explain Selenium architecture.

This is a very important interview question.

Selenium 4 architecture — simplified
Test Script
    ↓
Selenium WebDriver API
    ↓
W3C WebDriver Protocol
    ↓
Browser Driver
    ↓
Browser

For example:

Java Test
   ↓
Selenium WebDriver
   ↓
W3C WebDriver Protocol
   ↓
ChromeDriver
   ↓
Chrome Browser
🎯 Experienced Answer

"My Java automation code interacts with the Selenium WebDriver API. WebDriver communicates with the browser through the W3C WebDriver protocol. The corresponding browser driver, such as ChromeDriver, translates the commands into browser-specific actions and the browser performs them."

⭐ Important Selenium 4 point

Selenium 4 standardized communication around the W3C WebDriver standard.

197. WebDriver vs WebElement?

This is frequently asked.

WebDriver	WebElement
Represents the browser/session	Represents an element on the webpage
Controls browser	Controls individual element
Opens URL	Clicks/enters text
Manages windows	Gets text/attributes
Handles navigation	Handles element-level actions
driver.get()	element.click()
Example
WebDriver driver = new ChromeDriver();

WebElement username =
        driver.findElement(By.id("username"));

driver.get("https://example.com");

username.sendKeys("admin");

Here:

driver   → WebDriver
username → WebElement
🎯 Interview Answer

"WebDriver represents the browser session and is used for browser-level operations, while WebElement represents a particular DOM element and is used for element-level operations such as click, sendKeys and getText."

198. What is findElement()?

findElement() is used to locate a single web element.

Syntax
WebElement element = driver.findElement(By.id("username"));

Other locators:

driver.findElement(By.name("username"));

driver.findElement(By.className("login"));

driver.findElement(By.cssSelector("#username"));

driver.findElement(By.xpath("//input[@id='username']"));

driver.findElement(By.linkText("Login"));
Important behavior

findElement() returns the first matching element when multiple elements match the locator.

If no matching element is found, it throws:

NoSuchElementException
199. What is findElements()?

findElements() is used to locate multiple web elements.

It returns:

List<WebElement>
Example
List<WebElement> links =
        driver.findElements(By.tagName("a"));

Then:

for (WebElement link : links) {
    System.out.println(link.getText());
}

It is useful when we want to work with:

Multiple links
Table rows
Table columns
Checkboxes
Menu items
Search results
200. Difference between findElement() and findElements()?

🔥 Very common interview question.

findElement()	findElements()
Returns one WebElement	Returns List<WebElement>
Used for single element	Used for multiple elements
Returns first matching element	Returns all matching elements
If not found → NoSuchElementException	If not found → empty list
Direct element operations	Iterate/process collection
Example
WebElement login =
    driver.findElement(By.id("login"));

vs.

List<WebElement> buttons =
    driver.findElements(By.tagName("button"));
⭐ Interview trap

Don't say:

"findElement() always returns only one element."

More accurately:

"It returns a single WebElement, specifically the first matching element."

201. What happens if findElement() doesn't find an element?

It throws:

NoSuchElementException
Example
driver.findElement(By.id("wrongId"));

If the element doesn't exist, Selenium throws:

org.openqa.selenium.NoSuchElementException
🎯 Interview Answer

"If findElement cannot locate a matching element, Selenium throws NoSuchElementException."

⭐ Important

This is different from:

ElementNotInteractableException
ElementClickInterceptedException
StaleElementReferenceException

Those occur in different situations.

202. What happens if findElements() doesn't find an element?

It returns an empty list.

It does not throw NoSuchElementException just because there are no matching elements.

Example
List<WebElement> elements =
    driver.findElements(By.id("wrongId"));

System.out.println(elements.size());

Output:

0
🎯 Interview Answer

"If findElements doesn't find any matching elements, it returns an empty List<WebElement>, so we can safely check the list size before processing it."

Example
if (elements.isEmpty()) {
    System.out.println("Element not found");
}
203. Selenium 3 vs Selenium 4?

🔥 Very important for experienced SDET interviews.

Selenium 3	Selenium 4
Older architecture	Modernized architecture
JSON Wire Protocol was commonly associated	W3C WebDriver standard
Grid was more complex to configure	Grid 4 redesigned
Limited relative locator support	Relative locators
Older window/tab APIs	Improved/new window APIs
Older Actions capabilities	Improved Actions API
CDP support was limited	Stronger CDP integration
No Selenium Manager	Selenium Manager introduced
Major Selenium 4 improvements
W3C WebDriver standard
Selenium Grid 4
Relative locators
New tab/window APIs
Selenium Manager
Better DevTools integration
Improved Actions API
204. What are Selenium 4 features?

🔥 You should be able to explain at least these.

1. Relative Locators
driver.findElement(
    with(By.tagName("input"))
    .above(By.id("password"))
);

Common relationships include:

above()
below()
toLeftOf()
toRightOf()
near()
2. New Window / Tab API
driver.switchTo().newWindow(WindowType.TAB);

or:

driver.switchTo().newWindow(WindowType.WINDOW);
3. Selenium Grid 4

Grid was redesigned with improved architecture and support for distributed and parallel execution.

4. Selenium Manager

Selenium can automatically manage browser drivers in many standard setups, reducing the need to manually download/configure drivers.

For example, commonly:

WebDriver driver = new ChromeDriver();

without explicitly setting:

System.setProperty(...)

for the driver path.

5. Improved Actions API

Supports advanced:

Mouse actions
Keyboard actions
Pointer actions
Drag/drop
Hover
Key combinations
6. DevTools / CDP integration

Selenium 4 provides DevTools-related APIs for interacting with browser debugging capabilities.

205. What is WebDriver BiDi?

🔥 This is a modern Selenium interview topic.

WebDriver BiDi means WebDriver Bidirectional.

Traditional WebDriver communication is mainly request/response:

Test
 ↓
Browser command
 ↓
Browser
 ↓
Response

BiDi allows communication in both directions and supports event-driven browser information.

Conceptually:

Test  ↔  Browser

This is useful for things such as:

Browser events
Console events
Network events
Logs
Runtime information
🎯 Interview Answer

"WebDriver BiDi is the bidirectional browser automation protocol that extends WebDriver beyond the traditional request-response model. It allows automation code to receive browser events and interact with browser capabilities in a more event-driven way."

⭐ Don't confuse
WebDriver
   ↓
Standard browser automation

WebDriver BiDi
   ↓
Bidirectional + event-driven capabilities
206. What is CDP?

CDP = Chrome DevTools Protocol.

It is a protocol used by Chromium-based browsers to expose DevTools capabilities.

Selenium can interact with DevTools-related functionality through CDP.

Examples of CDP capabilities

Depending on browser/Selenium support, it can help with:

Network interception
Network conditions
Console/logging
Performance information
Browser emulation
Geolocation
Cookies
Security-related DevTools features
Example concept

You can emulate network conditions such as:

Offline
Slow network
Throttled network
🎯 Interview Answer

"CDP stands for Chrome DevTools Protocol. It provides access to Chromium browser DevTools capabilities such as network, performance, logging and emulation features. Selenium 4 provides DevTools integration that can be used when normal WebDriver APIs are not sufficient."

🔥 MOST IMPORTANT INTERVIEW DIFFERENCES

You should memorize these:

findElement() vs findElements()
findElement()
    ↓
WebElement
    ↓
Not found → NoSuchElementException
findElements()
    ↓
List<WebElement>
    ↓
Not found → Empty List
WebDriver vs WebElement
WebDriver
    ↓
Browser-level operations

WebElement
    ↓
Element-level operations
Selenium 3 vs Selenium 4

Remember:

W-R-G-R-M-C

W → W3C standard
R → Relative locators
G → Grid 4
R → new Window/Tab APIs
M → Selenium Manager
C → CDP/DevTools integration
