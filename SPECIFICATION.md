### Speedy 0.5.0 Specification

## Introduction

# What is Speedy?

Speedy is a new metadata format, intended to be easier to read and parse than JSON, while natively supporting as many data types as possible. This is so that applications can easily work together, without having to ask the user what format the data is in - for example, if it is a date or not.

# What is Speedy useful for?

Speedy can be used in any place where metadata is useful; for example, a large amount of files in one directory that need to be organised.

# Encoding

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

## Document Language tag

This tag is optional, but it is helpful when you make multiple copies of the same data, just in different languages, and you need to quickly parse them. It always goes at the very beginning of the document, and is an ISO 639-3 language code after an exclamation mark (!).

**Example:**

If a document was in Dutch, the document would begin:

        !nld;

## Data types

The supported data types are strings, numbers, booleans, nulls, dates & times, arrays, languages, and files.

# Strings

Strings are surrounded by double quote signs (").

**Example:**

        string: "Hello, world!";

For simplicity, there is only one escape sequence: `\"`. This enables strings to be as short as possible, while at the same time enabling applications to perform easy checks to find the end of a string.

**Example:**

        escapeString: "She said, \"I wonder where I'll go today?\"";

# Numbers

Numbers may only use the decimal digits 0 through 9, the minus sign (-), and the decimal point (.). Hexadecimal, octal, and binary values are not natively supported; instead, these should be placed within strings.

**Example:**

        num: 123;

Negative numbers are stored with a minus sign just before the first digit.

**Example:**

        negative: -456;

Floating point numbers have a decimal point between the integer and the fraction.

**Example:**

        float: 789.01;

# Booleans

Booleans are formatted as simply true or falce, without quotation marks.

**Example:**

        bool: false;

# Nulls

Nulls are simply the word "null".

**Example:**

        null: null;

# Date & time

Date and time can be stored with a number; however, there is a built-in method to handle them, to make them easier to scan for. They are formatted as `YYYYMMDDHHMMSS`, with a letter "d" at the front, using 24-hour time.

**Example:**

        datetime: d20160226153000;

Note that depending on the precision required, values can be left off the end. Here is an example which is only precise down to the day:

        date: d19980212;

If timezones are required, they may be added with a little plus (+) or minus (-) sign at the end, followed by a float specifying the number of hours away from UTC. If this is not there, nothing is assumed.

**Examples:**

        datetimezone1: d20150930043012-6;
        datetimezone2: d20151001195623+8.5;

# Arrays

Arrays are surrounded by square brackets (\[ and \]). Each member of the array is separated by a comma (,).

**Example:**

        array: ["This is an array!", 3, true, d19700101];

Arrays may be used as data in a different variable by writing the array name and then the location of the data, surrounded in square brackets. Arrays are zero indexed.

**Example:**

        data5: array[3];

This would call the date from the previous array.

# Languages

Languages are useful if a database needs to determine the particular language of a text document, for example. The format is very similar to describing the language of the Speedy document itself.

**Example:**

        language: !eng;

# Files

The location of files can be just a string, but like dates, there is a built-in method. Start the value with a forward slash (/), before the name and extension of the file. Spaces in the file name are dealt with using a backslash (\).

**Example:**

        file1: /file.txt;
        file2: /long\ file\ name.speedy;

Only files in the same directory as the Speedy file may be formatted this way. This is to ensure maximum compatibility with all file systems.

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
