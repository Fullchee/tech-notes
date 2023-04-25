# Browser JavaScript

## Sub-resource integrity

```html
<script src="//cdnjs....."
 integrity="sha256-..."
crossorigin="anonymous">
```

if the CDN gets hacked, then the script won't run

## [Get the URL params](https://stackoverflow.com/a/901144/8479344)

```javascript
// ?q=turtles or window.location.search
search_string = new URL("https://www.google.ca/search?q=turtles&oq=tortuga");
search_string = new URL(window.location.search);

params = new URLSearchParams(search_string);

params.get("q"); // "turtles"
const { q } = Object.fromEntries(params);
```

!!! Note: Object.fromEntries only works for regular keys

## JS Event Handler

### Keyboard event

-   [keypress](https://developer.mozilla.org/en-US/docs/Web/API/Element/keypress_event): deprecated
-   use [keydown](https://developer.mozilla.org/en-US/docs/Web/API/Element/keydown_event) or [keyup](https://developer.mozilla.org/en-US/docs/Web/API/Element/keyup_event)

#### Spacebar vs Enter

-   spacebar: trigger event on keyup
-   enter: trigger on keydown

https://www.clairecodes.com/blog/2019-11-06-the-roles-of-spacebar-and-enter-in-keyboard-navigation/

Spacebar
- activate buttons
- check/uncheck
- scroll down the page
- expand a dropdown menu

Enter
- activate buttons
- open links
- open menus

| Element to access | Key                   |
| ----------------- | --------------------- |
| Link              | - Enter               |
| Button            | - Enter<br>- Spacebar |

Don't need generics because we aren't using custom properties of an HTMLInputElement for example

```typescript title="buttonA11yProps.ts"
const triggerClickOnKeyboardEvent =
    (triggerKeys: string[]) => (e: React.KeyboardEvent<HTMLElement>) => {
        if (triggerKeys.includes(e.key)) {
            e.preventDefault();
            e.target.click();
        }
    };

export const triggerClickOnEnterKey = triggerClickOnKeyboardEvent(["Enter"]);
export const triggerClickOnSpacebar = triggerClickOnKeyboardEvent([" "]);

/**
 * @example
 * <div
 *    onClick={() => {})}
 *    {...clickOnEnterOrSpacebarProps}
 *    className="clickable other-classes"
 * />
 * >
 *
 * @example
 * <div
 *    onClick={() => {})}
 *    {...clickOnEnterOrSpacebarProps}
 *    onKeyDown={() => { console.log('Custom onKeyDown')}}
 * />
 */
export const clickOnEnterOrSpacebarProps = {
    role: "button",
    className: "clickable",
    tabIndex: 0,
    onKeyDown: triggerClickOnEnterKey,
    onKeyUp: triggerClickOnSpacebar,
};
```


## How to download JSON file?

[Download JSON object as a file from browser - Stack Overflow](https://stackoverflow.com/a/30800715/8479344)

- Create an `<a>` tag and click it and then remove it
- set the href to 

```javascript
    var dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(exportObj));
```


### Console API

https://developer.chrome.com/docs/devtools/console/api/

```javascript
console.log("%cMessage", "color: orange; background-color: blue");
```

#### [Coloured console.log](https://mmazzarolo.com/blog/2022-08-25-simple-colored-logging-for-javascript-clis/?utm_source=stefanjudis)

```js
console.success = (...args) => console.log("\x1b[32m✔\x1b[0m", ...args);
console.failure = (...args) => console.error("\x1b[31mｘ\x1b[0m", ...args);
```

```js
const logger = {
    ...console,
    success: (...args) => console.log("\x1b[32msuccess\x1b[0m", ...args),
    failure: (...args) => console.error("\x1b[31mfailure\x1b[0m", ...args),
};

logger.success("Files copied successfully");
logger.failure("Unable to delete the 'system32' directory");
```


## $ Chrome dev tools shortcuts

>[!$()]-
>document.querySelector

>[!$$()]-
>document.querySelectorAll()

>[!$0]-
>the most recently selected element in the Elements tab

>[!$_()_]-
>most recently evaluated expression in the console

