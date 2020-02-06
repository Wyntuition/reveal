# An Intro to Property-based Testing

### Featuring junit-quickcheck

--

## What is property-based testing? 

PBT is a way to write automated tests that focuses on a property of functionality

--

## Why bother?

Typical unit tests with defined inputs are often called example-based tests

--

```
@Test
public void answer_invalid_from_long_value_example_based() {
  final String input = StringUtils.repeat("Hello world", 100);

  var result = BasicAnswerValidation.textIsValidLength()
    .apply(input);

  assertFalse(result.isValid());
  assertEquals(
      "Didn't fail validation as notValid",
      "answer.invalidSize",
      result.getReasons().iterator().next().getMessageKey());
}
```

--

```
@Test
public void answer_invalid_from_short_value_example_based() {
  final String input = "";

  var result = BasicAnswerValidation.textIsValidLength()
    .apply(input);

  assertFalse(result.isValid());
  assertEquals(
      "Didn't fail validation as notValid",
      "answer.invalidSize",
      result.getReasons().iterator().next().getMessageKey());
}
```

--

```
@Test
public void answer_invalid_from_null_value_example_based() {
  final String input = null;

  var result = BasicAnswerValidation.textIsValidLength().apply(input);

  assertFalse(result.isValid());
  assertEquals(
      "Didn't fail validation as notValid",
      "answer.invalidSize",
      result.getReasons().iterator().next().getMessageKey());
}

```

--

* Data-driven test solve when you need to test for several different sets of input, but don't want all the code of a test for each

* With PBT, the inputs are more dynamic, and often based on the type of input

--

## Generators 

Input is created via generators. Many come OOTB, and you can make your own. 

--

Introducing `junit-quickheck`

```
@Property
public void answer_invalid_from_invalid_value(
    @NullAllowed(probability = 1.0f) String input) {
  
  final String freeFormAnswer = input;

  var result = BasicAnswerValidation.textIsValidLength()
    .apply(input);

  assertFalse(result.isValid());
  assertEquals(
      "Didn't fail validation as notValid",
      "answer.invalidSize",
      result.getReasons().iterator().next().getMessageKey());
}
```

--

## History

* PBT came out of the functionality community
* Haskell quickcheck
* Pure functions are good candidates for PBT
* Available in *Java, Scala, Python, F#, Haskell...*

--

When to use it

--

* Numerous different combinations of inputs that may lead to unexpected behaviors. A lot of logic with a lot of various behaviors based on different inputs of the same type
* Exploratory testing, legacy code

--

When not to use it

--

* When examples are easy to define
* When defined examples reliably cover the functionality
* Integration testing with large number of inputs

--

### Resources

* junit-quickcheck, https://github.com/pholser/junit-quickcheck
* Interview with Bill Venners on Property Based Testing, https://www.se-radio.net/2018/05/se-radio-episode-322-bill-venners-on-property-based-tests/
* Blog on Property-based Testing against a Poker app, https://www.leadingagile.com/2018/04/step-by-step-toward-property-based-testing/

Thanks!

--



DEMO:
Poker one, or Person, or 
Functional: scala with nomanclature 

## Marvelous List

*   No order here
*   Or here
*   Or here
*   Or here

---

## Fantastic Ordered List

1.  One is smaller than...
2.  Two is smaller than...
3.  Three!

---
