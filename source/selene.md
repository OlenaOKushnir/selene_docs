<meta http-equiv="refresh" content="6; url=https://yashaka.github.io/selene/"/>

# Selene API

```{eval-rst}
.. include:: includes/redirect-banner.rst
```

[[src]](https://github.com/yashaka/selene)

The core of the Selene library. Main methods are ```open_url```, ```s``` and ```ss```:

## ```open_url```

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

After you receive a SeleneElement object be the "s" command, you can perform some actions or actions with it:
```
s('#toggle-all').click()
```

```
s('#new-todo').set_value(task_text).press_enter()
```
or check some condition:
```
s('#todo-count').should(have.text('3'))
```

If we are looking for a specific element from a group of the same type, it is convenient to use the command ```"ss"```

For example, instead of a long expression

```
s("//*[@id='todo-list']/li[.//text()='b']//*[@class='toggle']").click()
```

you can use a much more readable chain of methods

```
ss('#todo-list>li').element(by.exact_text('b')).find('.toggle').click()
```

Another plus of such chains of methods is that we get a more informative error message. It makes it possible to identify which of the "links" of the chain did not work. In the first version, we get only a message that the method did not work.


In case you need to reuse some parts elsewhere - go ahead and move your locators:

```
tasks = ss("#todo-list>li")
active = have.css_class("active")
completed = have.css_class("completed")
```
