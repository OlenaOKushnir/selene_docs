# SeleneCollection

The object of the SeleneCollection class is a "proxy", like [SeleneElement](http://selene-docs-test.readthedocs.io/en/latest/elements.html#). To call it, you need to call the ```ss``` method. The result is the list of web-elements on the page.

```
ss('#todo-list>li')
```

We can filter Collections by some condition, check the state of elements collection, get statuses and attributes.

## Assertions

Just as for SeleneElement for SeleneCollection there are condition checks(```should(be.Condition)``` or ```should(have.Condition)```). As a result, the SeleneCollection object is returned and it is possible to build chains of calls.

The SeleneCollection class also has a special type of check - the correspondence of each individual element from the list to a specific condition (```should_each(be.Condition)``` or ```should_each(have.Condition)```):

```
ss(".srg .g")[0].should(have.text("In Greek mythology, Selene is the goddess of the moon"))

ss('#todo-list>li').should(have.size(3))

ss('#todo-list>li').should(have.exact_texts("1", "2", "3")).
    should_each(have.css_class("active"))
```

These methods also have built-in implicit waits. Within 4 seconds (by default) they wait for the condition to be satisfied.

## Methods to get statuses and attributes of elements collection

You can use such methods to get statuses and attributes of SeleneCollection:

+ ```texts(texts)```

+ ```exact_texts(texts)```

+ ```size(index)```

+ ```empty()```

+ ```size_at_least(index)```

[Examples](http://selene-docs-test.readthedocs.io/en/latest/collection_condition.html)

## Methods-selectors of specific collection elements

Additionally, you can sort the resulting collection by some condition:

```filtered_by(Condition)``` | ```all_by(Condition)```  | ```filtered(Condition)```  | ```filter_by(Condition)``` | ```ss(Condition)```

returns the proxy-collection that represents elements of original collection filtered by condition

e.g. ```ss('.item').filtered_by(text('foo'))```

```element_by(Condition)``` | ```find_by(Condition)``` | ```s(Condition)```

returns the first element of the collection that matches the condition

e.g. ```ss('.item').element_by(text('foo'))```

Some more useful methods for working with SeleneCollection:

```size()``` - returns size of collection

```first()``` - returns first element of collection
