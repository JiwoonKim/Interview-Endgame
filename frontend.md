# :star: Frontend Interview Questions & Answers

| No. | Questions |
|:---|:---|
| | What is a single-page applications(SPA)? |
| | What is ECMAScript? |
| | What is Babel? |
| | What is a package manager? |
| | __Webpack__ |
| 1 | What is Webpack? |
| 2 | What does a bundler do? |
| 3 | What is code-splitting? |

## Title

?. ### What is a Single-page Application (SPA)?
   A single-page application is an application where 

## Webpack

2. ### What does a bundler do?
   A bundler __merges imported files into a single file__. The resulting “bundle” can then be included on a webpage __to load an entire app at once__.
   
   - App
   
   ```js
   // app.js                            // math.js
   import { add } from './math.js';     export function add(a, b) {
                                          return a + b;
   console.log(add(16, 26)); // 42      }
   ```
   
   - Bundle
   ```js
   function add(a, b) {
     return a + b;
   }

   console.log(add(16, 26)); // 42
   ```

3. ### What is code-splitting?
   Code splitting is the __process of splitting code into various bundles to optimze load performance__. By splitting code into small chunks, the application can
   - __reduce initial load time__ since it can leave out unnecessary code at the timing
   - __lazy-load to improve performance__ to load just the things currently needed at the moment
   
   Code-splitting does not reduce the overall amount of code, however, 

