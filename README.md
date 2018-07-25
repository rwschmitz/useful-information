# Repository Purpose
This repository will contain information such as:
- Explanations behind why certain concepts, functions, methods, properties, etc. work the way they do.
- Useful code snippets and a brief explanation as to what they do.

## Wordpress

### Built-in Methods

- the_post();
    - This method iterates through an array, essentially.
    - It acts similarly to the unary operator, `++`.
    - Due to it's similarity to `++`, it kind of turns the `while` loop into a `for` loop.
    - **Use case:** while in a `while` loop, `the_post();` will iterate through the array until the `while` loop condition is false and exits.
    - [Link to Wordpress Documentation](https://developer.wordpress.org/reference/functions/the_post/)
