<meta http-equiv="refresh" content="6; url=https://yashaka.github.io/selene/"/>

# PageObjects

```{eval-rst}
.. include:: includes/redirect-banner.rst
```

If you did not like the "non-OOP" module functions from above, don't panic, you can use the same API via creating SeleneDriver objects...

## PageObjects implementation

Here is a simple example of PageObjects implementation (inspired by [selenide google search example](https://github.com/selenide-examples/google/tree/master/test/org/selenide/examples/google/selenide_page_object)):

```
from selene.browser import open_url
from selene.support.jquery_style_selectors import s, ss
from selene.support.conditions import have

class GooglePage(object):
    def open(self):
        open_url('http://google.com/ncr')
        return self

    def search(self, text):
        s("[name='q']").set(text).press_enter()
        return SearchResultsPage()

class SearchResultsPage(object):
    def __init__(self):
        self.results = ss('.srg .g')

def test_google_search():
    google = GooglePage().open()
    search = google.search('selene')
    search.results[0].should(have.text
      ('In Greek mythology, Selene is the goddess of the moon'))  # :D
```

That's it. Selene encourages to start writing tests in the simplest way. And add more layers of abstraction only by real demand.

## PageObjects composed with Widgets

Sometimes your UI is build with many "reusable" widgets or components. If you follow general "Test Automation Pyramid" guidelines, most probably you have not too much of automated selenium tests. And "simple pageobjects" will be pretty enough for your tests. But in case you need to write a tone of UI tests, and you need correspondent DRY solution for your reusable components then this section may be for you.

Selene encourages to use composition over inheritance to reuse parts of web application like sidepanels, headers, footers, main contents, search forms, etc. This especially may be usefull in the case of over-complicated single-page applications. Consequently we can naturally model our app under test even with a SinglePageObject composed with Widgets, that can be loaded on demand.

Below you can find an example of Widgets (aka ElementObjects, aka "PageObjects by Fowler". The application under test - TodoMVC is very simple. It is completely does not make sense to use Widgets here:). But we use it just as an example of implementation.

```
from selene.conditions import exact_text, hidden, exact_texts
from selene.browser import set_driver, driver
from selene.support.jquery_style_selectors import ss, s
from selenium import webdriver
from selene.support.conditions import have, be

from helpers.todomvc import given_active


def setup_module(m):
    set_driver(webdriver.Firefox())


def teardown_module(m):
    driver().quit()

class Task(object):

    def __init__(self, container):
        self.container = container

    def toggle(self):
        self.container.element(".toggle").click()
        return self


class Tasks(object):

    def _elements(self):
        return ss("#todo-list>li")

    def _task_element(self, text):
        return self._elements().element_by(have.exact_text(text))

    def task(self, text):
        return Task(self._task_element(text))

    def should_be(self, *texts):
        self._elements().should(have.exact_texts(*texts))


class Footer(object):
    def __init__(self):
        self.container = s("#footer")
        self.clear_completed = self.container.element("#clear-completed")

    def should_have_items_left(self, number_of_active_tasks):
        self.container.element("#todo-count>strong").
             should(have.exact_text(str(number_of_active_tasks)))


class TodoMVC(object):
    def __init__(self):
        self.container = s("#todoapp")
        self.tasks = Tasks()
        self.footer = Footer()

    def clear_completed(self):
        self.footer.clear_completed.click()
        self.footer.clear_completed.should(be.hidden)
        return self


def test_complete_task():
    given_active("a", "b")

    app = TodoMVC()

    app.tasks.task("b").toggle()
    app.clear_completed()
    app.tasks.should_be("a")
    app.footer.should_have_items_left(1)
```

## More examples

See [/tests/](https://github.com/yashaka/selene/tree/master/tests) files for more examples of usage. E.g. one more [PageObject with Widgets example](https://github.com/yashaka/selene/blob/master/tests/examples/order/app_model/order_widgets.py) and its [acceptance test](https://github.com/yashaka/selene/blob/master/tests/examples/order/order_test.py).
