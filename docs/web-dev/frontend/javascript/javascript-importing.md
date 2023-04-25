# JavaScript importing

## History of importing

-   CommonJS
    -   `exports.myFunction = myFunction`
    -   `const myFunction = require("myFile").myFunction`
    -   how Node.js was
-   AMD
    -   async module definitions
    -   [Dojo](https://dojotoolkit.org/)
-   [ES Modules](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)

## Barrel files

```javascript
import { Card, SectionHeader } from "@src/Common";
```

```javascript
import { Card } from "@src/Common/Components/Card";
import { SectionHeader } from "@src/Common/Components/SectionHeader";
```

-   avoid using barrel files
-   if you ever want to code split, import directly from the file
