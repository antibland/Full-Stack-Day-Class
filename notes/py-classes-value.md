# Value Classes
All the Python built-in types are interpreted as **value types**:
if the contents are the same, they are equal.
```python
5 == 3  #> False
[1, 2, 3] == [1, 2, 3]  #> True
{'cat': 4, 'snake': 0} == {'cat': 4, 'snake': 0}  #> True
```

But the classes you make, _aren't_ by default.
Python doesn't assume you have the same definition of equals.

You should make them work that way _if it makes sense_, though.
It's much easier to think about.

Write a **magic eq** function in your class to define equality.
It must have the signature `__eq__(self, other)` and _return_ a bool.
```python
class AddressBookEntry:
  def __init__(self, name, phone_number):
    self.name = name
    self.phone_number = phone_number

  def __eq__(self, other_entry):
    return (
      self.name == other_entry.name and
      self.phone_number == other_entry.phone_number
    )
```

Python will magically call this function for you whenever the first argument to `==` is that type.
```python
me = AddressBookEntry('David', '507-555-9895')
you = AddressBookEntry('Helen', '507-555-2131')

# These two lines run the same code:
me == you  #> False
AddressBookEntry.__eq__(me, you)  #> False
```

Because of this, note:
```python
me == 5  # throws AttributeError
```
I think that's okay.
You should _avoid_ comparing different types.
An error will remind you.

## Is that right?
Not every class makes sense as a value type.
Think about whether two instances should be equal if all their data is equal.
Some types don't make sense like that; e.g. an `Account` class that _doesn't_ have a unique ID in it.
