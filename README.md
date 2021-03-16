# Repository Purpose
This repository will contain information such as:
- Explanations behind why certain concepts, functions, methods, properties, etc. work the way they do.
- Useful code snippets and a brief explanation as to what they do.
- Useful articles that explain concepts in detail.

## JavaScript

### General Information

#### The keyword `this`

- The instance of `this` is not bound in an arrow function.
- The instance of `this` **IS** bound to a regular function.
- Example:
    ```
      const coolOuterFunction = () => {
        const coolImage = new Image();
        coolImage.onload = function innerFunction() {
           console.log(this) // this is scoped to innerFunction()
       }
      }
     ```
     ```
      const coolOuterFunction = () => {
        const coolImage = new Image();
        coolImage.onload = () => {
           console.log(this) // this is scoped to coolOuterFunction()
       }
      }
     ```
- [Codepen Example](https://codepen.io/rwschmitz/pen/RqVNVR)

### Articles

#### Classes, new, instanceof, prototype chains and API design by Dan Abramov

- [How Does React Tell a Class from a Function](https://overreacted.io/how-does-react-tell-a-class-from-a-function/)

#### Using .call() and .apply()

- [Changing The Execution Context Of JavaScript Functions Using Call() And Apply()](https://www.bennadel.com/blog/2265-changing-the-execution-context-of-javascript-functions-using-call-and-apply.htm)

#### JavaScript Algorithms

- [JavaScript Algorithms](https://github.com/trekhleb/javascript-algorithms)

#### General React Information

- [React Resources](https://reactresources.com/)

#### JavaScript Clean Code - Best Practices

- [JavaScript Clean Code - Best Practices](https://devinduct.com/blogpost/22/javascript-clean-code-best-practices)

### Api Design

#### Post Request

- Incoming post requests will contain data, and this data can be put on the post body.
- If using axios on the FE, an example would be:  `axios.post(url, { data: { someKey: 'someValue' } } )`
- In your API on the backend, you can access this data with `req.body` and see `someKey: 'someValue'`
- Alternatively, when you post data on the FE, you can put this data in query params.

## React

### General Information

#### API Querying

- API calls to 3rd party APIs should be made in the `componentDidMount() {}` method.

### Helper Functions

#### importImages
- Grab images from within the project directory to map over
- `const importImages = r => ( r.keys().map(r) )`
- `const images = importImages(require.context('../img/<Directory>', false, /\.(png|jpe?g|svg)$/));`

## PHP

### Syntax

- `<?= $variable; ?>` is equivalent to `<?php echo $variable; ?>` -- It's just convenient shorthand.

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
    
## WooCommerce

### General Information

#### OAuth 1.0 Authentication over HTTP

  - Create API key in the Wordpress admin with Read/Write access.
  - Enable legacy REST API.
  - Hit the following endpoint: `<your url here>/wc-api/v3/products`
  - To change the number of results returned, go to:  Wordpress admin -> Settings -> Reading -> "Blog pages show at most".
  - `oauth_consumer_key`, `oauth_nonce`, `oauth_timestamp`, `oauth_signature_method` and `oauth_version` are all used together at the same time to generate the OAuth 1.0 signature.
  - Use built-in Node.js `crypto` library with the following:  `const crypto = require('crypto');`
  - Use OAuthSignature NPM package at the following link: [NPM Package Link](https://www.npmjs.com/package/oauth-signature)
  - Using the above package, the following snippet of code can be used:  `const encodedSignature = OAuthSignature.generate(requestMethod, requestURL, parameters, consumerSecret);`
  - The `parameters` variable is made up of:  `oauth_consumer_key`, `oauth_nonce`, `oauth_timestamp`, `oauth_signature_method` and `oauth_version`
  - If all settings are correct and the OAuth signature is being generated correctly, you can use the Axios library.  Axios is at the following link:  [NPM Package Link](https://www.npmjs.com/package/axios)

## Filestack

### General Information

#### Accessing the JSON Response

  - `onPick` is the method that is called to allow uploading.
  - Use the `onSuccess` property and pass in `response` for the parameter.
  - In the return, access the url specifically with `response.filesUploaded[0].url`.
  - You can access other parts of the JSON response by looking into `response.filesUploaded[0]`.
  
## CORS

### General Information

#### Creating a Canvas from External Server Content

  - Create canvas with `const yourNewCanvas = document.createElement('canvas');`
  - Define the width and height of the canvas
  - Create the context for the canvas with `const yourNewContext = yourNewCanvas.getContext('2d');`
  - Create a new image with `const yourNewImage = new Image();`
  - **VERY IMPORTANT** -- Set the attribute on your new image BEFORE defining the src.
      - `yourNewImage.setAttribute('crossOrigin', 'anonymous');`
      - `yourNewImage.src = <insert your 3rd party content as the source here>;`
  - Call the `drawImage()` method on `yourNewContext` like so:  `yourNewContext.drawImage(yourNewImage, ...define widths and heights here)`
  - You may now turn the new canvas into a blob and resolve the blob to an image
  - `return new Promise((resolve, reject) => {`
      `canvas.toBlob(file => {`
      `file.name = fileName;`
      `resolve(file);`
      `}, 'image/jpeg');`
    `});`

## Shopify

### Forms

#### Adding a custom CSS class to Shopify forms

- There is a class filter you can hook into.
- Example:  `{% form 'create_customer', class: 'CUSTOM_CLASS_HERE' %}`

## NVM

### Seeing all releases of Node

- `nvm ls-remote`

## Strapi

### Table information persists

- Even when you delete something out of the UI portion of the CMS, the name remains in the database.

### Column character limit in Postgres

- The limit is 63 characters, so name your columns accordingly.

### Upload limit

- The max upload limit for the asset library is initially restricted by your Nginx conf file.
- Go to `/etc/nginx/nginx.conf`
- Make the following change:
```
http {
  client_max_body_size 10M;
}
```
- This will change the upload size to 10MB.
