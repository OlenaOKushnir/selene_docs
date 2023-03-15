<meta http-equiv="refresh" content="6; url=https://yashaka.github.io/selene/"/>

# Quick Start

```{eval-rst}
.. include:: includes/redirect-banner.rst
```

## Basic Usage: 4 pillars of Selene

All Selene API consists just from 4 pillars:

1. Browser Actions (including finding elements)
2. Custom Selectors
3. Assertion Conditions
4. Custom Configuration

And one more not mandatory bonus:

   5.Concise jquery-style shortcuts for finding elements  

All pillars are reflected in corresponding selene python modules and their methods.

## 1. Browser Actions: [browser.* ](https://github.com/yashaka/selene/blob/master/selene/browser.py)

e.g. ```browser.open_url('https://todomvc4tasj.herokuapp.com')```

e.g. ```browser.element('#new-todo')```

e.g. ```browser.all('#todo-list>li')```

Once you have the elements, of course you can do some actions on them:

e.g. ```browser.element('#new-todo').set_value('do something').press_enter()```

e.g. ```browser.all('#todo-list>li').first().find('.toggle').click()```

## 2. Custom Selectors: [by.* ](https://github.com/yashaka/selene/blob/master/selene/support/by.py)

By default element finders (```browser.element```, ```browser.all```) accept css selectors as strings, but you can use any custom selector from the ```by``` module.

e.g. ```browser.element(by.link_text("Active")).click()```

## 3. Assertion Conditions: [be.* ](https://github.com/yashaka/selene/blob/master/selene/support/conditions/be.py) and [have.* ](https://github.com/yashaka/selene/blob/master/selene/support/conditions/have.py)

Assertion conditions are used in "assertion actions" on elements.

e.g. ```browser.element('#new-todo').should(be.blank)``` or the same ```browser.element("#new-todo").should(have.value(''))```

e.g. ```browser.all('#todo-list>li').should(have.exact_texts('do something', 'do more'))```

e.g. ```browser.all('#todo-list>li').should(be.empty)```

## 4. Custom Configuration: [config.* ](https://github.com/yashaka/selene/blob/master/selene/config.py)

e.g. ```config.browser_name = 'chrome'```

You can omit custom configuration and Selene will use default values, e.g. ```browser_name``` is equal to ```'firefox'``` by default

Config options can be also overriden with corresponding system variables (see [#51](https://github.com/yashaka/selene/issues/51) for more details)

##  + 5. Concise jquery-style shortcuts for finding elements

e.g. ```s('#new-todo')``` instead of ```browser.element('#new-todo')```

e.g. ```ss('#todo-list>li')``` instead of ```browser.all('#todo-list>li')```

## Imports

You can access to all main Selene API via single "wildcard" import:

```
from selene.api import *
```

If you don't like "wildcard" imports, you can use direct module imports or direct module functions import;) no problem:)
