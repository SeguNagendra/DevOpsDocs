---
sidebar_position: 9
---

## JSON Fundamentals for API Testing
### Automation Tester Perspective

JSON (**JavaScript Object Notation**) is the **most common data format** used in REST APIs.
For automation testers, understanding JSON is mandatory to **validate responses correctly and avoid fragile assertions**.

---

## What is JSON?

JSON is a **lightweight, text-based data format** used to exchange data between client and server.

Example:
```json
{
  "userId": 101,
  "name": "John",
  "active": true
}
```

---

## JSON Data Types

| Type | Example |
|---|---|
| String | "John" |
| Number | 101, 99.5 |
| Boolean | true / false |
| Null | null |
| Object | { } |
| Array | [ ] |

Tester tip:
> Always validate **type + value**, not just value.

---

## JSON Object

An **object** is a collection of key–value pairs.

```json
{
  "id": 101,
  "email": "john@gmail.com"
}
```

Automation usage:
- Validate specific fields
- Assert mandatory keys exist

---

## JSON Array

An **array** is an ordered list of values or objects.

```json
[
  { "id": 1 },
  { "id": 2 }
]
```

Automation usage:
- Validate list size
- Validate at least one matching object
- Avoid fixed index assertions unless required

---

## Nested JSON (Very Common)

```json
{
  "order": {
    "id": 5001,
    "items": [
      {
        "productId": 10,
        "price": 299
      }
    ]
  }
}
```

Tester focus:
- Navigate nested structures correctly
- Validate inner objects and arrays

---

## JSON Path Basics (Conceptual)

JSON Path is used to locate data inside JSON.

Examples:
```
$.id
$.order.items[0].price
$.users[*].email
```

Tester rule:
> Use JSON paths that are **resilient to order changes**.

---

## Common JSON Validation Patterns

### Field Existence
- Key exists
- Value not null

### Value Validation
- Exact match
- Range check
- Enum validation

### Array Validation
- Size > 0
- Contains expected object

---

## Null Handling in JSON

```json
{
  "middleName": null
}
```

Tester considerations:
- null ≠ missing key
- Validate expected nulls explicitly
- Avoid NullPointer-like assumptions

---

## Common Automation Mistakes ❌

- Assuming fixed array index
- Ignoring null values
- Comparing entire JSON blindly
- Not validating data types

---

## Best Practices for JSON Validation ✅

- Validate only required fields
- Avoid full response comparison
- Use flexible JSON paths
- Separate schema vs data validation
- Log response on failure

---

## Interview-Ready Questions

**Q: Difference between missing key and null?**  
A: Missing key does not exist; null exists with no value.

**Q: Why avoid fixed index in arrays?**  
A: Order may change, causing flaky tests.

---

## Key Takeaways 🎯

- JSON is the standard API data format
- Objects, arrays, and nesting are common
- Validation should be flexible
- Type awareness prevents bugs
- Good JSON handling = stable API tests