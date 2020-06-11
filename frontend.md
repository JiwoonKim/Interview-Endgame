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
   Code splitting is the __process of splitting code into various bundles to optimze load performance__. While it does not reduce the overall amount of code, an application can split code into small chunks to
   - __reduce initial load time__ since it can leave out unnecessary code at the timing
   - __lazy-load to improve performance__ to load just the things currently needed at the moment
   
   Code splitting especially comes handly for SPAs since it can lazy-load only the necessary code for the inital page and __leave out other pages and components not used at the moment__, solving the heavy intial load issue of SPAs. 
   
   Even on the inital page, code splitting can further improve load performance by only loading parts of the code necessary at the moment and dynamically loading code necessary later on. For example, if there is a form component as the inital page and a third party library is used to check an input when it is inserted, the library code can be left out of the inital load. Later, the library code can be dynamically loaded when the user actually inserts input. This helps to reduce the inital load time when the bundles are large and especially when using third party libraries in the code.

   - reference: https://web.dev/reduce-javascript-payloads-with-code-splitting/
