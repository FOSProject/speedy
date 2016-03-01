# Speedy 0.1.2 Specification

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

The current supported data types are strings, integers, boolean values, null values, and dates.

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

### Dates

Dates can obviously just be stored with a simple integer, but this is the more official way to do it: format them YYYYMMDD, and put a "d" at the front. This makes it much easier to quickly scan for a date and find them as fast as possible.

**Example:**

    d20160226