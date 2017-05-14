# Condition

[[src]](https://github.com/yashaka/selene/blob/master/selene/conditions.py)

Conditions in Selenium wait for a certain condition (visible, enabled, text ('some text')) 4 seconds (default) or the time assigned by the user.

Which one to use?

```tasks.should(be.Condition)``` | ```tasks.should(have.Condition)```

or

```tasks.assure(Condition)``` | ```tasks.should_be(Condition)```


All the following names means the same: ```assure```, ```should```, ```should_be```, ```should_have``` (or ```assure_not```, ```should_not```, ```should_not_be``` , ```should_not_have```).

Just the first assure sounds good with any condition:

```
assure(visible) :)
assure(text('foo') :)
```

but others may not:

```
should(visible) :(
should(text('foo')) :(
```

so you have to choose proper "condition" version each time:

```
should(be.visible :)
should(have.text('foo')) :)
```

or proper "should" alias:

```
should_be(visible) :)
should_have(text('foo')) :)
```

though these versions are less laconic than when using assure. Compare:

```
assure(text('foo') :)
should_have(text('foo')) :|
should(have.text('foo')) :|
```

But regardless being less concise, the latest version gives you better autocomplete abilities when you don't remember all conditions:

```
assure(. :(
should(have. ... :)
```

There seems to be no "the only best option". You can use the style you prefer more;)

```
s('input').should(exist)
s('input').should(be.visible)
s('input').should(have.exact_text('Some text'))
```

```s('#element')```  +  ```should(be.condition)``` or ```should(have.condition)```

Usage:

```
visible | appear // e.g. s('#new-todo').should(be.visible)

hidden | disappear | not(visible) // e.g. s('.destroy').should(be.hidden)

clickable // e.g. s(".button").should(be.clickable)

enabled // e.g. s('#new-todo').should(be.enabled)

in_dom | exist // e.g. s(".input").should(be.in_dom)

text(String substring) // e.g. s('#element').should(have.text(‘foo’))

exact_text(String wholeText) // e.g. s('#element').should(have.exact_text(‘foo’))

css_class(String) // e.g. s('.element').should(have.css_cl('nav'))

attribute(name, value) // e.g. s('.element').should(have.attribute('class', 'g'))

value // e.g. s('.element').should(have.value('text')
```

Any condition can be negated:

```ss('.item').filtered_by(not (exact_text)).size()```
