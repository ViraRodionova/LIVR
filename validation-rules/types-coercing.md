### Types coercing

You should treat rules as expectations.  Therefore, all implementation make types coercing in numeric rules. This is reasonable because if someone says "positive\_integer" then he expects to receive positive integer after validation.

We follow the same logic for string rules.  We compare values as string as rule are "string rules" but return what developer expects.  For example, if we use "eq" rule with input:

```text
{
    field1: 1,
    field2: 1
}
```

and rules:

```text
{
    field1: {eq: "1"},
    field2: {eq: 1},
}
```

output will be:

```text
{
    field1: "1",
    field2: 1
}
```

[\(demo\)](http://webbylab.github.io/livr-playground/#{"rules"%3A"{\n   field1%3A {eq%3A 1}%2C\n   field2%3A {eq%3A \"1\"}%2C\n}"%2C"data"%3A"{ \n    field1%3A 1%2C \n    field2%3A 1\n}"})

_What about the test suite? The test suite is stored in JSON format, therefore we can rely only on types that are supported by JSON. So, if we have input {field: "1"}, rules {field: 'positive\_integer'} then the output will be { field: 1 }. As I see it should work. For example, JavaScript will coerce "1" to 1. And the test will pass. Perl will do nothing. And the test will pass. Please, let me know if there are any issues with this._

Standard rules that should be supported by every implementation:

* Common Rules
  * required
  * not\_empty
  * not\_empty\_list
  * any\_object
* String Rules
  * string
  * eq
  * one\_of
  * max\_length
  * min\_length
  * length\_between
  * length\_equal
  * like
* Numeric Rules
  * integer
  * positive\_integer
  * decimal
  * positive\_decimal
  * max\_number
  * min\_number
  * number\_between
* Special Rules
  * email
  * url
  * iso\_date
  * equal\_to\_field
* Metarules
  * nested\_object
  * list\_of
  * list\_of\_objects
  * list\_of\_different\_objects
  * or
* Modifiers \(previously - "Filter rules"\)
  * trim
  * to\_lc
  * to\_uc
  * remove
  * leave\_only
  * default


