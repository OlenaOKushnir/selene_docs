<meta http-equiv="refresh" content="6; url=https://yashaka.github.io/selene/"/>

# WebDriverRunner

```{eval-rst}
.. include:: includes/redirect-banner.rst
```

[ [src] ](https://github.com/yashaka/selene/blob/master/selene/conditions.py)

Some browser management methods and conditions:

+ ```js_returned_true(script_to_return_bool)``` - checks whether a script returns 'true'

+ ```title(exact_value)``` - checks whether an actual title matches the expected title

+ ```title_containing(partial_value)``` - checks whether an actual title contains the expected title

+ ```url(exact_value)``` - checks whether an actual url matches the expected url

+ ```url_containing(partial_value)``` - checks whether an actual url contains the expected part of url

+ ```set_driver(webdriver)``` - tells Selene to use driver created by the user
