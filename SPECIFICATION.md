# Speedy 0.9.0 Specification

## Introduction

### What is Speedy?

Speedy is a new data serialisation format, intended to be easier to read and parse than JSON, while still being as useful in as many applications as possible.

### What is Speedy useful for?

Speedy can be used to create metadata formats that need to be as transparent as possible, such as the deta project.

### Encoding

Speedy is strictly UTF-8 encoded. This is to ensure maximum compatibility and simplicity, as well as longevity; this also helps save space in areas where this is a concern.

## The basic structure

Any data formatted using Speedy is always given a variable. This appears before the data, with a colon (:) placed at the end to signify the end. The data is then stored, followed by a semicolon (;) to signify the end of the data.

**Example:**

        data1: "Hello, world!";

Best practice is to list all the individual data on separate lines; however, if storage is a concern, whitespace is not required. These carry the same information:

        name: "Dan";
        age: 23;

and

        name:"Dan";age:23;

## Data types

The supported data types are strings, ints and floats, booleans, and nulls.

### Strings

Strings are surrounded by double quote signs. (").

**Example:**

        string: "Hello, world!";

For simplicity, there is only one escape sequence: `\"`. This enables strings to be as short as possible, while at the same time enabling applications to perform easy checks to find the end of a string.

**Example:**

        escapeString: "She said, \"I wonder where I'll go today?\"";

### Numbers

Numbers may only use the decimal digits 0 through 9, the minus sign (-), and the decimal point (.). Hexadecimal, octal, and binary values are not natively supported; instead, these should be placed within strings.

**Example:**

        num: 123;

Negative numbers are stored with a minus sign just before the first digit.

**Example:**

        negative: -456;

Floating point numbers have a decimal point between the integer and the fraction.

**Example:**

        float: 789.01;

### Booleans

Booleans are formatted as simply true or falce, without quotation marks.

**Example:**

        bool: false;

### Nulls

Nulls are simply the word "null".

**Example:**

        null: null;

## Nested data

Nested data may be used for simple databases. For example, if a database of names and ages was being stored, one could simply hold the data like this:

        user1: {
                name: "Sarah";
                age: 26;
        };
        user2: {
                name: "Tim";
                age: 27;
        };

In order to call the data or reference it in another part of the document, you can simply call the variables according to their nested positions; for example, `user1.name` or `user2.age`.

## Comments

Single-line comments are supported in Speedy. To make a comment, a line should be ended with an octothorpe (#).

**Example:**

        price: 5.00; # dollars and cents

Currently, multi-line comments are not supported.
