# Ink Language Parser

Develop a simple parser in your preferred programming language that can read and
interpret basic constructs of the [Ink narrative
language](https://www.inklestudios.com/ink/) which is an English like language
to write interactive fictions.

The idea of this exercise is to learn writing parsers and understand connected
challenges. The recommended way to go about this exercise is to first write the
parser from scratch (starting from pure RegEx) and the use common parsing
frameworks or approaches.

Here are a few expectations from your program:

+ Your parser library (or cli tool) should expose two functions, `parse` for
  taking Ink string and returning a structured data, and `format` for taking
  structured Ink data and returning formatted Ink string.
+ It should be able to recognize and handle basic Ink syntax, such as:
    + Knots and Diverts (e.g., `== knot_name -> divert_target`)
    + Choices (e.g., `* [Choice 1] Text of choice 1`)
    + Conditional logic (e.g., `{ condition: True branch | False branch }`)
+ Implement informative error handling for unrecognized syntax.

!!! warning "Testing"

    There are no tests for this exercise as of now. You should write your own example Ink
    samples and check something like `format(parse(original_text)) == original_text`

!!! tip

    Since you are writing the parser for Ink, you can also make a CLI tool that executes
    the story. You can take design inspiration from [Inky](https://github.com/inkle/inky).

## Resources
1. [Ink Homepage](https://github.com/inkle/ink)
2. [Reference implementations in C#](https://github.com/inkle/ink/tree/master/compiler/InkParser)
