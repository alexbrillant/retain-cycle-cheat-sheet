# Retain Cycle Cheat Sheet

## #1: An object must never retain its parent

An object should never retain its parent when it makes a pointer to the parent.

Solution : use weak reference
```
  class Parent {
    var name: String
    var child: Child?
    init(name: String) {
      self.name = name
    }
  }
  
  class Child {
    var name: String
    weak var parent: Parent!
    init(name: String, parent: Parent) {
      self.name = name
      self.parent = parent
    }
  }
```

## #2: No hierarchical ancestor can be retained

An object must not retain any of its parent's parents, or any of their parents.

## #3: "Connection" objects should not retain their target

Any object which connects itself to an arbitrary target object, without knowing their relationship, must not retain its target.

## #4: Use "close" methods to break cycles

If you have a hierarchy that is difficult to work out, it may be easier to retain any object you wish, and implement a "close" method to address the problem of cycles.

## #5: temporary retains must be temporary

Any of these rules can be broken for short periods of time — however the rule must by "unbroken" automatically, without further intervention, for example: when an animation or other triggered process completes.
