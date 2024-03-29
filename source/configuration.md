<meta http-equiv="refresh" content="6; url=https://yashaka.github.io/selene/"/>

# Configuration

```{eval-rst}
.. include:: includes/redirect-banner.rst
```

[ [src] ](https://github.com/yashaka/selene/blob/master/selene/config.py)

This class contains different configuration options to configure execution of Selene-based tests, e.g.:

+ ```timeout```: waiting timeout in seconds, that is used in explicit (should/should_not/wait_for) and implicit waiting in Selene; set to 4 ms by default; can be changed for specific tests
    e.g. ```config.timeout = 6```

+ ```app_host```

   e.g. ```config.app_host = 'http://chromedriver.storage.googleapis.com'```

+ ```browser_name```(by default it`s "firexox")

   e.g. ```config.browser_name = 'chrome'```

+ ```_default_folder```

+ ```hold_browser_open```

...
