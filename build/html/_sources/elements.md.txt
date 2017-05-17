# SeleneElement
[ [src] ](https://github.com/yashaka/selene/blob/master/selene/elements.py)

The object returned by the ```s``` command is called a "proxy-element". The SeleneElement class is a wrapper around Selenium WebElement, which adds some very useful methods. At the moment of creation of proxy-element the real search of element on the page is not initiated. But on any subsequent action or condition check - the actual replica of the page element will be acquired by the "proxy-element", and the corresponding action or condition check will be "proxied" to it.

This allows to automate testing of modern dynamic web applications.
You can also store the "proxy-element" into the PageObject field before loading the corresponding page in the browser:

```
# before opening a browser and loading a page url
from selene.api import *
from selene.bys import by_link_text


class HomePage(object):

    menu = s('#menu')

    def filter_active(self) :
      self.menu.element(by_link_text('Active')).click()

    def toggle_all(self):
      self.menu.element("#toggle-all").click()

    def test(self):
        home = HomePage()
        # now the s command was executed and the SeleneElement object was created,
        but the browser has not been opened yet
        # ...
        open("/home")
        # the browser has been opened and the page has been loaded
        home.filter_active()
        # exactly here the search was initiated and the actual replica of the page menu element was got,
        then its inner stream element was found and the click command was "proxied" to it.
        # ...something else might happen
        home.toggle_all()
        # and now, before finding the element-link with the "Active" text to
        click on it - again, the actual version of the menu element was found on the page.

```

There are such methods for for the SeleneElement:

- inner elements search methods (the methods for creating proxy-elements that represents corresponding inner elements)
- methods to check element state - assertions
- methods-actions on element
- methods to get element statuses and attribute values
- others

All these methods has some built-in features for their convenient usage. The majority of them has built-in implicit waits.

## Inner elements search methods

```
s(String cssSelector) | element(String cssSelector)
s(by.*) | element_by(by)
ss(String cssSelector) | all(String cssSelector)
ss(by.*) | elements_by(by)
```

Here ```s``` and ```ss``` are just synonyms of ```element``` and ```all``` methods correspondingly.

All these methods return "proxy-elements", they will not start the search of actual elements on the page until you call some action like ```.click()```.

So you can build whole "locators chains", getting one element inside another:

```
s('#menu').element(".edit")..all('.item')
```

You can also save such "locators chains" in variables. And no matter how long they are, whether the browser is open and a page is already loaded or not

```
# before opening the browser and loading the page
from selene.api import *
from selene.bys import by_link_text

class HomePage(object):

    menu = s('#menu')
    active = menu.element(by_link_text('Active'))
    toggle = menu.element('#toggle-all')

    # ...
    open("/home")
    # loading the page (in automatically opened browser)
    active.click()
    # ...
    toggle.click()
    # ...
```

## Methods to check element state - assertions


Assertions methods serve for verification. This method trigger the search of actual element on a page, then it is checked on the condition(an object the [Condition class](https://github.com/yashaka/selene/blob/master/selene/conditions.py)). It returns back the object of SeleneElement.

```tasks.should(be.Condition)``` | ```tasks.should(have.Condition)```. More details about asserts you can find [here](http://selene-docs-test.readthedocs.io/en/latest/condition.html)


## Methods-actions on element

Element actions methods:

```
+ click()

+ double_click()

+ context_click()

+ hover()

+ set(String) | set_value(String)

+ scroll_to()

+ press_enter()

+ press_escape()

+ press_tab()
...
```

All these methods perform corresponding action after the search for proxy-elements on the page.
And each of these actions has a built-in implicit wait for the element's visibility (the default value of config.timeout is 4 seconds).
As a result you don't need to check the element's visibility everytime.

Instead of code

```s('.destroy').shouldBe(visible).click()```

you write just

```s('.destroy').click()```.

The majority of actions allow you to build method chains also:

```s('#edit').set_value('new_text_value').press_enter()```.

## Methods to get element statuses and attribute values


These methods trigger the search of actual element on a page. Some of them have built-in implicit waitings (wait for availability in DOM, even if method is hidden on the page):

e.g.

```
text()

is_selected()

is_enabled()

location_once_scrolled_into_view()

size()

location()

rect()
```

The following methods do not wait:

```
tag_name()

get_attribute(String)

is_displayed()

value_of_css_property(String)

parent()

id()
```
