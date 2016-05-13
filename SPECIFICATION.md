# Speedy 0.1.8 Specification

## Introduction

Speedy is a data serialisation format, intended to be easier to read and parse than JSON, while natively supporting as many data types as possible. This is so that applications can easily work together, without having to ask the user what format the data is in - for example, if it is a date or not.

Speedy is strictly UTF-8 encoded. This is to ensure maximum compatibility and simplicity, as well as longevity.

## The basic formatting of Speedy

Any data formatted using Speedy is always given a name first. This name appears before the data, with a colon (:) placed at the end to signify the end of the name. The data is then stored, followed by a semicolon (;) to signify the end of the data.

**Example:**

        data1: "Hello, world!";

Nested data structures are supported. The nest starts with the root name, then an opening brace ({), then the nested structure, and finally a closing brace (}).

**Example:**

        data2: {
                data3: "Hello, world!";
                data4: "Example text";
        };
    
These are more fully documented in the "Nested data" section.

## Document language

This tag is optional, but it is helpful when you make multiple copies of the same data, just in different languages, and you need to quickly parse them. It always goes at the very beginning of the document, and is an ISO 639-3 language code after an exclamation mark (!).

For example, if a document was in Dutch, the document would begin:

        !nld

## Data types

The current supported data types are strings, integers, boolean values, null values, dates, arrays, and languages.

### Strings

Strings are surrounded by double quote signs ("), and act like strings normally would.

**Example:**

        "Hello, world!"

There are currently five escape sequences: `\"`, `\;`, `\{`, `\}`, and `\:`.

**Example:**

            "She said, \"I wonder where I'll go today?\""

### Numbers

Numbers may only use the decimal digits 0 through 9, the minus sign (-), and the decimal point (.).

**Example:**

        123

Negative numbers are stored with a minus sign just before the first digit.

**Example:**

        -456

Floating point numbers have a decimal point between the integer part and the fractional part.

**Example:**

        -789.01

### Boolean values

Booleans are formatted as simply true or false, with no double quotes.

**Example:**

        false

### Null values

Nulls are simply the word "null".

**Example:**

        null

### Date & time

Date and time can obviously just be stored with a simple integer, but this is the more official way to do it: format them YYYYMMDDHHMMSS, and put a "d" at the front. Use 24 hour time, too. This makes it much easier to quickly scan for a date and find them as fast as possible.

**Example:**

        d20160226153000
    
This is fine if you only expect this to be local, but with a more global program it's trickier due to timezones. In order to fix this, a little + or - sign is added at the end, along with a float saying the amount of hours away from UTC. If there is no number, nothing is assumed.

**Examples:**

        d20150930043012-6
        d20151001195623+8.5

### Arrays

Arrays are surrounded by square brackets ("[" and "]"). Each member of the array is separated by a comma (,).

**Example**:

        ["Array", 3, true, d19700101100000]

You can use one of these as a piece of data in a different variable by writing the array name and then the location of the data, surrounded in square brackets. Arrays are zero indexed.

**Example:**

If we wanted to call the date from the previous array named "array":

        data5: array[3];

### Languages

Languages are useful if a database needs to determine the particular language of a text document, for example. The format is very similar to describing the language of the actual Speedy document, except it's not placed at the top.

        language: !nld;

## Nested data

Nested data can be used if we wish to use the same variable names for multiple values. For example, if a database of names and ages was being stored, one could simply hold the data like this:

        user1: {
                name: "Sarah";
                age: 26;
        };
        user2: {
                name: "Tim";
                age: 27;
        };

In order to call the data or reference it in another part of the Speedy document, you can simply call the variables according to their nested positions; for example, `user1.name` or `user2.age`.

## Comments

Single-line comments are supported in Speedy. Currently, the supported way is to end a line with a #. For example:

        price: 5.00; # dollars and cents

Currently, multi-line comments are not supported.
