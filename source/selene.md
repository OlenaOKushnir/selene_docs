# Selene

[[src]](https://github.com/yashaka/selene)

The core of the Selene library. Main methods are ```open_url```, ```s``` and ```ss```:

## open_url

To visit page you can just specify url:

```browser.open_url('http://chromedriver.storage.googleapis.com/index.html?path=2.9')```

But it is better to specify base url and use relative urls to visit pages:

```config.app_host = 'http://chromedriver.storage.googleapis.com'```

```browser.open_url('/index.browser.open_urlhtml?path=2.9')```

## ```s``` and ```ss```

```s(cssSelector)``` – returns object of the SeleneElement class that represents first element found by CSS selector on the page.

```s(by.*)``` – returns "first SeleneElement" by the locator of the By class

```ss(cssSelector)``` – returns object of type ElementsCollection that represents collection of all elements found by a CSS selector.

```ss(by.*)``` – returns "collection of elements" by the locator of By type

You can also use alias methods for your taste:

 ```
 tasks[2].s(".toggle").click()
 ```

instead of

```
tasks[2].element(".toggle").click()
```

Usually, when you get a SeleneElement object be the "s" command, you can perform some action on it:
```
s('#toggle-all').click()
```
and even several actions at once:
```
s('#new-todo').set_value(task_text).press_enter()
```
or check some condition:
```
s('#todo-count').should(have.text('3'))
```

```"ss"``` can be useful when a needed element is a one of a same type. For example, instead of:

```
s("//*[@id='todo-list']/li[.//text()='b']//*[@class='toggle']").click()
```

you can use a more readable and verbose alternative:

```
ss('#todo-list>li').element(by.exact_text('b')).find('.toggle').click()
```

Such a "composite locator" is also convenient because in the case of an error in finding an element, it makes it possible, according to the error message, to immediately determine which of the "parts" did not work. In the first case, we can only get information that the "whole locator" did not work, and we will spend more time searching for the "part" that led to the error.

In case you need to reuse some parts elsewhere - go ahead and move your locators:

```
tasks = ss("#todo-list>li")
active = have.css_class("active")
completed = have.css_class("completed")
```
