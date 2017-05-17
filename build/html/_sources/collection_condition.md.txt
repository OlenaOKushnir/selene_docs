# Collection Conditions

The following check models are used:  


**SeleneCollection + should(have.Condition) or should(be.Condition)**

**SeleneCollection + should_not(have.Condition) or should_not(be.Condition)**  


In Selene are presented such methods to get statues and attributes for collections:

+ ```texts(texts)```

   e.g. ```ss('#todo-list>li').should(have.texts('a', 'c', 'e'))```

+ ```exact_texts(texts)```

   e.g. ```ss('#todo-list>li').should(have.texts('ab', 'cd', 'ef'))```

+ ```size(index)```

   e.g. ```ss('#todo-list>li').should(have.size(3))```

+ ```empty()```

   e.g. ```ss('#todo-list>li').should(be.empty)```

+ ```size_at_least(index)```

   e.g. ```ss('#todo-list>li').should(have.size_at_least(3))```
