
198. What is findElement()?
findElement() is used to locate a single web element.

Syntax
WebElement element =
        driver.findElement(By.id("username"));

Other Locators
driver.findElement(By.name("username"));

driver.findElement(By.className("login"));

driver.findElement(By.cssSelector("#username"));

driver.findElement(By.xpath("//input[@id='username']"));

driver.findElement(By.linkText("Login"));

Important Behavior
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

⭐ Interview Trap
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

Output
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

Major Selenium 4 Improvements
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

6. DevTools / CDP Integration
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

⭐ Don't Confuse
WebDriver
   ↓
Standard browser automation

WebDriver BiDi
   ↓
Bidirectional + event-driven capabilities

206. What is CDP?
CDP = Chrome DevTools Protocol

It is a protocol used by Chromium-based browsers to expose DevTools capabilities.

Selenium can interact with DevTools-related functionality through CDP.

Examples of CDP Capabilities
Depending on browser/Selenium support, it can help with:

Network interception

Network conditions

Console/logging

Performance information

Browser emulation

Geolocation

Cookies

Security-related DevTools features

Example Concept
You can emulate network conditions such as:

Offline
Slow network
Throttled network

🎯 Interview Answer
"CDP stands for Chrome DevTools Protocol. It provides access to Chromium browser DevTools capabilities such as network, performance, logging and emulation features. Selenium 4 provides DevTools integration that can be used when normal WebDriver APIs are not sufficient."

🔥 MOST IMPORTANT INTERVIEW DIFFERENCES
These are the comparisons you should memorize.

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

W → W3C Standard
Selenium 4 uses the W3C WebDriver standard.

R → Relative Locators
Examples:

above()
below()
toLeftOf()
toRightOf()
near()

G → Grid 4
Selenium Grid was redesigned in Selenium 4.

R → New Window/Tab APIs
newWindow(WindowType.TAB)
newWindow(WindowType.WINDOW)

M → Selenium Manager
Helps manage browser drivers automatically in standard setups.

C → CDP / DevTools Integration
Provides access to browser DevTools-related capabilities.
