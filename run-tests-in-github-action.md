Run tests in github action
___

1. Add headless and watch false task in the `package.json`:
    ```
      "test:ci": "ng test --watch=false --browsers=ChromeHeadless"
    ```
