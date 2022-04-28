# Transforming data with DataWeave

Find here the scripts or snippets used for Chapter 6, Transform with DataWeave.

You can either copy and paste from this README directly, or you can go to the corresponding file.

## Using operators

`mathematical-operators.dwl`

```dataweave
%dw 2.0
output application/dw
---
{
    Addition: {
        DateTimes: |2020-01-01| + |P2D|, // = |2020-01-03|
        Numbers: 1 + 2, // = 3
        Array: ["a", "b"] + "c" // = ["a", "b", "c"]
    },
    Subtraction: {
        DateTimes: |2020-01-03| - |P1D|, // = |2020-01-02|
        Numbers: 3 - 1, // = 2
        Array: ["a", "b", "c"] - "a", // = ["b", "c"]
        Object: { k1:"v1", k2:"v2" } - "k1" // = { k2: "v2" }
    },
    Multiplication: {
        Numbers: 3 * 3 // = 9
    },
    Division: {
        Numbers: 9 / 3 // = 3
    }
}
```

`equality-and-relational-operators.dwl`

```dataweave
%dw 2.0
output application/dw
---
{
    LessThan: {
        Strings: "a" < "b", // true
        Booleans: true < false, // false
        Numbers: 1 < 2, // true
        DateTimes: |2020-01-01| < |2022-01-01| // true
    },
    GreaterThan: {
        Strings: "a" > "b", // false
        Booleans: true > false, //true
        Numbers: 1 > 2, // false
        DateTimes: |15:00:00| > |13:00:00| // true
    },
    LessOrEqualTo: {
        Strings: "a" <= "a", // true
        Booleans: true <= true, // true
        Numbers: 1 <= 1, // true
        DateTimes: |2020-01-01| <= |2020-01-01| // true
    },
    GreaterOrEqualTo: {
        Strings: "a" >= "a", // true
        Booleans: true >= true, // true
        Numbers: 1 >= 1, // true
        DateTimes: |2020-01-01| >= |2020-01-01| // true
    },
    EqualTo: {
        Strings: "a" == "b", // false
        Booleans: true == false, // false
        Numbers: 1 == 1, // true
        DateTimes: |2020-01-01| == |2020-01-01T10:00:00|, // false
        Nulls: null == null, // true
        Arrays: [1, 2, 3] == [1, 2, "3"], // false
        Objects: {a:"1"} == {a:1}, // false
        DiffTypes: 1 == "1" // false
    },
    SimilarTo: {
        Strings: "true" ~= true, // true
        Booleans: false ~= "false", // true
        Numbers: 1 ~= "1", // true
        DateTimes: |2020-01-01| ~= |2020-01-01T10:00:00|, // true
        Nulls: null ~= null, // true
        Arrays: [1, 2, 3] ~= [1, 2, "3"], // true
        Objects: {a:"1"} ~= {a:1}, // true
        DiffTypes: 1 ~= "1" // true
    }
}
```