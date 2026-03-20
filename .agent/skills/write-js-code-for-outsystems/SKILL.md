---
name: write-js-code-for-outsystems
description: Use this skill when the user asks to write or optimize JavaScript code for OutSystems.
---

# Instructions

## For JavaScript code optimization

- Read the code and list the business logic it performs.
- Analyze the request and determine which part of the code will be modified.
- Suggest the section to be changed. Note: if more than 50% of the code base must be modified, you need to reassess and ask the user for additional context.

## For code generation (including optimization), follow these rules

- Do not use the spread operator.
- Always assume every variable has a default value. Nothing is truly infinite; there will always be a finite value that can be determined. Exceptions: operations like element search may accept null or undefined.
- OutSystems accepts the following data types: Text, Integer, Long Integer, Decimal, Boolean, Date Time, Date, Time, Phone Number, Email, Binary Data, Object, Currency.
- The execution function must always be named main().
- All other function definitions must be placed below main().
- Inputs of a Node JS in OutSystems can be accessed via the $parameters variable.
- Example: If a Node JS has two inputs, FirstName and LastName, they can be accessed as $parameters.FirstName and $parameters.LastName.
- Do not use the var keyword.
- Use const whenever possible; otherwise, use let.
- External inputs passed into the node must be declared at the start of main() with the prefix pr.
- Example:
    const prFirstName = $parameters.FirstName
    const prLastName = $parameters.LastName
- Do not use semicolons (;) at the end of lines.
- Ensure null safety.
- All functions with inputs and outputs (except main) must be written in a testable way, especially calculation functions.
- Constants must be written in CAPS with underscores, e.g.:
    const THIS_IS_A_CONST = 12
- For JS Nodes with outputs, always place the output assignment at the end of main(). Prefix outputs with out.
- Example:

```js
    $parameters.OutAge = outAge
    $parameters.OutNumberOfCrew = outNumberOfCrew
```

- Document the function at the start of main() with a summary of the user’s request.
- Input and output declarations at the start of main() must begin with comments // INPUTS and // OUTPUTS.
- Example:

```js
    function main() {
      // INPUTS
      ... Declare inputs here

      ... Implement logic here

      // OUTPUTS
      ... Declare outputs here
    }
```

- All other functions must follow JS Docs standards (see: [https://jsdoc.app/](https://jsdoc.app/)).
- When modifying code, ask for the user’s account name. Then generate a comment for each change using the template:
    `<AccountName> - <CurrentDate> - <Description of change in English or Japanese>`
- Example:

```js
    // XinTA - 2026/03/20 - This is a change
```

- For long comments, use multi-line format:

```js
/**
* XinTA - 2026/03/20 - This is a change
* A loooooooooooooooooooooooog comment
*/
```

- For if-else statements, prefer false-first logic.
- Avoid:

```js
    if (variable != null) {
        
    } else {
        
    }
```

- Prefer:

```js
    if (variable == null) {
        ...
    } else {
        ...
    }
```

- Inform the user if there are unhandled branches in an if statement.
- In addition to local variables and input/output parameters, the following predefined objects are available in the JavaScript execution context (all prefixed with $):
- $parameters – Contains input and output parameters defined for the current JS element.
- $actions – References to client actions callable within the current JS element.
- $roles – Contains all custom roles defined for the current application.
- $public – Contains objects instantiated from all classes and modules of the JavaScript API in public mode. See the JavaScript API Reference for the full list.
- Standard browser objects (window, document, JSON, RegExp) may also be used.
- Indent 4 with spaces.

## Constraints

- For each user request, when optimizing code, do not modify more than 50% of the code base.
- If there is a risk of having to change 50% of the code, you must ask at least 2 questions to the user to confirm the scope and improve the context.
- Do not use external libraries; all generated code must be Vanilla JS. If it is absolutely necessary to use an external library, you must make the user aware of:
- Installing a usable version of that library on OutSystems
- Importing the JS library as a minified file into the Scripts folder of Service Studio
