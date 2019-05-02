### Indentation 
- Use 4 spaces / any space that your language of choice recommends
- Code is meant to be read, please use add newlines + indentation to split long code statements / long method calls, imagine, do you prefer reading an long article and scorll horizontally or vertically?

```java
// Bad, ugh :(, make reading great again!
ResultFromExternalLibrary result = this.someExternalLibrary.doSomethingWithParameter(parameter1, parameter2, parameter3);

// Bad, opening parenthesis does not match the current
// statement indentation level,
// this way indentation guide won't match the closing parenthesis.
// If the description is confusing, let me know and
// I'll show you how the indentation guide helps.
ResultFromExternalLibrary result = this.someExternalLibrary.doSomethingWithParameter(
  parameter1,
  parameter2,
  parameter3);



// Good,
ResultFromExternalLibrary result = this.someExternalLibrary.doSomethingWithParameter(
  parameter1,
  parameter2,
  parameter3
  );
```

### Builder pattern
Please create DTO / builder pattern for method (no function in java) with >= 2 parameters.
You could use lombok plugin to automatically create builder for you.

```java
// :')
AnnuityCalculator.calculate(100000, 0.1, 3);

// Yes it's longer, but you can guess what's the parameters for and it fixes
// the possibility of bug because of wrong parameter ordering
// e.g. AnnuityCalculator.calculate(3, 0.1, 100000);
AnnuityCalculator.calculate(
  FooBarInput
    .builder()
    .principal(100000)
    .interestRate(0.1)
    .tenure(3)
    .build()
);

// It's arguable that 2-parameter method to use Builder pattern,
// but consider this method, which one is the discount? first one or 2nd one?
// by convention it should be 120000 and amount should be named purchaseAmount,
// but it doesn't prevent engineer to do this kind of mistake.
DiscountCalculator.subtractDiscount(amount, 120000)

// Now imagine we're stricting builder pattern
// Note that there's no strict indentation for for the SubtractDiscountInput,
// you can place it at the same line of .subtractDiscount method call,
// or you could add new line (just like AnnuityCalculator.calculate example above),
// it's up to you :)
// Please note that for a 2-parameter method, if the parameter type is different then
// you don't need to use builder pattern.
DiscountCalculator.subtractDiscount(SubtractDiscountInput.builder()
    .purchaseAmount(amount)
    .discount(120000)
    .build()
)
```

### Guard pattern
Not many language has `guard` keyword / feature, in that case you could emulate the same with any language. Imagine that you're preventing something to happen and you're using nested ifs, note that nested code is harder to read and harder to maintain, it also introduces more indentation means more horizontal scrolling. The key to emulate `guard` is by using `if`, `return` and `throw` (if the language is using exception)


```java
// My gosh, 2 nested statements, the business logic is
// wrapped with 2 levels of curly brackets :scream:
if (valid) {
  if (discount != 0) {
      // Logic here
      return bla bla;
  } else {
      // Another logic
      return bla bla;
  }
} else {
  // Throw error
}

// Guard statement to rescue!
// Not only it's easier to read but it's easier to extract & refactor the "branching" logic inside the if statement
// to another function/method.
if (!valid) {
  // Throw error
}

if (discount != 0) {
  // Logic here
  return bla bla;
}

// Main logic here
return bla bla;
```

### Naming convention for certain data structures
#### Variables
##### Iterable
Use plural for iterable data type such as `Array`, `List`, `Set`

Good
```
posts
users
```

Bad
```
post
user
```

##### Map / Dictionary
Use `<value>By<Key>` format for `Map` / `Dictionary` type

Good
```
// If we supply email as key, we will get a user
userByEmail

// If we supply product type as key, we will get an iterable products
productsByProductType
```

Bad
```
users
user
products
product
```

#### Comments
- Always use capital letter to start a new sentence
- Add one space between comment marker and the comment itself

Good
```
// This is a comment.
// Another comment.
```

Bad
```
//This is a comment
// this is a comment
```

#### File Nodes
Use hyphen `-` or underscore `_` to separate words

Never use
- space, makes it harder for autocompletion in terminal
- camelCase, macOS is not case sensitive.

Good
```
some-file.txt
some_file.txt
```

Bad

```
someFile.txt
some file.txt
```


#### Urls
Use `-` to separate words

Good

```
http://example.com/some-example/post
```

Bad

```
http://example.com/some_example/post
http://example.com/some example/post
```

