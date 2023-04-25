[[Backend - What happens when you go to Google]]

[Google tool: Measure page quality](https://web.dev/measure/)

Renders the HTML page

-   See the Performance tab
-   Calculates the DOM from HTML
    -   JS representation
    -   Scripts block the parser
        -   Unless they're marked as async or defer
-   CSSOM from CSS
    -   JS representation
    -   Blocked by downloading CSS
-   Calculates the ???
    -   Combines DOM and CSSOM
-   Calculate the render tree
    -   Might be blocked by the resources you're downloading
- Creates the a11y tree
-   Calculates layout from render tree
    -   Flow, flexbox, grid
-   Paints the pixels
-   ![89f233ea32dc5fba5edb096698d16c20.png](89f233ea32dc5fba5edb096698d16c20.png "89f233ea32dc5fba5edb096698d16c20.png")
