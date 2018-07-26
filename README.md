# Repository Purpose
This repository will contain information such as:
- Explanations behind why certain concepts, functions, methods, properties, etc. work the way they do.
- Useful code snippets and a brief explanation as to what they do.

## PHP

### Syntax

- `<?= $variable; ?>` is equivalent to `<?php echo $variable; ?>` -- It's just convenient shorthand

### Helper Functions

#### fancyDataLogging();
- Display logged data in a more readable format to the browser window.
- `function fancyDataLogging($variable) { highlight_string("<?php\nloggedData =\n" . var_export($variable, true) . ";\n?>"); }`

## Wordpress

### Built-in Methods

- the_post();
    - This method iterates through an array, essentially.
    - It acts similarly to the unary operator, `++`.
    - Due to it's similarity to `++`, it kind of turns the `while` loop into a `for` loop.
    - **Use case:** While in a `while` loop, `the_post();` will iterate through the array until the `while` loop condition is false and exits.
    - [Developer -- Link to Wordpress Documentation](https://developer.wordpress.org/reference/functions/the_post/)
    
- body_class();
    - This method will allow you to pass in a `string` or `array` to the body.
    - **Use case:** If you want to dynamically add CSS classes to the body based on whatever conditional, you can use this method.
    - [Developer -- Link to Wordpress Documentation](https://developer.wordpress.org/reference/functions/body_class/)
    
- wp_reset_postdata(); 
    - By default, there is a main WP_Query running.
    - By making a secondary WP_Query (`$query = new WP_Query( $args )`), you are no longer on the current page's data.  You're on whatever page is being returned by the new, secondary WP_Query.
    - In order to return back to the current page's data, you have to use `wp_reset_postdata();` to gain access to other built-in Wordpress methods again.
        - Examples are using the Wordpress methods that start with `the_`, such as `the_title();` or `the_content();`
    - **Use case:** If you're on page A, and you want data from page B, you can create a new query.  Once done with page B's data, you can return to page A with this method.
    - [Codex -- Link to Wordpress Documentation](https://codex.wordpress.org/Function_Reference/wp_reset_postdata)
