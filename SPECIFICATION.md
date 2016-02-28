# Speedy 0.1.0 Specification

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

## Data types

The current supported data types are strings, integers, boolean values, and null values.

### Strings

Strings are surrounded by double quote signs ("), and act like strings normally would.

**Example:**

    "Hello, world!"

There are currently five escape sequences: `\"`, `\;`, `\{`, `\}`, and `\:`.

**Example:**

    "She said, \"I wonder where I'll go today?\""

### Integers

Integers may only use the decimal digits 0 through 9. Currently, there is no support for negative or floating-point numbers, however this is planned in the future.

**Example:**

    123

### Boolean values

Booleans are formatted as simply true or false, with no double quotes.

**Example:**

    false

### Null values

Nulls are simply the word "null".

**Example:**

    null
