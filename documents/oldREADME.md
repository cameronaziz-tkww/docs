---
---
---
---
**Old Readme**

To run a single test:
```
docker-compose run --rm test yarn test <test file>
```
For example:
```
docker-compose run --rm test yarn test apps/marketplace-web/client/pages/VendorsSearch/containers/test.js
```

Debugging
- The following command will build the test and then wait for you to open the Node debugger in Chrome or VS Code.  You can then resume execution and place breakpoints in the debugger, VS Code, or in the code with `debugger` statements
```
docker-compose run --rm test yarn test:debug <test file>
```