# End to End Test

## Where is the document for End-to-End test?

* [End-to-End test document](https://teams.microsoft.com/_#/docx/viewer/teams/https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture~2FShared%20Documents~2FGeneral~2Fauto-test~2Fe2etest_handbook.docx?threadId=19%3Ae81ccb01ec2e48f9b6f4fd21da53fad6%40thread.skype&baseUrl=https%3A~2F~2Fa10networks.sharepoint.com~2Fsites~2FGUIFuture&fileId=CC8F2496-CCCB-4CCF-AA05-CCFE5F8922F7&ctx=files&viewerAction=view)​

## Why did the DOM element not change after clicking it by using the .click\(\) function to send a click command to WebDriver?

If you can locate the DOM element correctly, but cannot access the callback function by clicking on it, it may be because the element is not shown in the viewable area of the browser.

You can use .execute\(\) function to run a JavaScript code in browser to show the DOM element in a viewable area of the browser.

```typescript
  browser
    .execute(
      // this function is send to the browser and run in it, so it can not get any variable in you E2E test code.
      // if it needs to use some values in your E2E test code, you should push them in a Array as the second param.
      // it will receives these data sequentially as its parameters.
      function(param1, param2) {
          // 1. locate the DOM element
        const div = document.getElementById(param1)
        const switchBtn = div.getElementsByClassName(param2)[0]
        // 2. use scrollIntoView to move the element to viewable area
        switchBtn.scrollIntoView(true)
        return
      },
      [param1, param2],
      () => {
        // do something else after running the JavaScript code
      }
    )
```

## How do I run a specific project?

1. Create a new config file like `nightwatch.config.dashboard.dev.js`
2. Change the codepath and rootpath

```typescript
const codePath = path.resolve(__dirname, 'tests/e2e/dist/Dashboard/')
const rootPath = path.resolve(__dirname, 'tests/e2e/dist/')

module.exports = {
  src_folders: [codePath],
  output_folder: 'reports/testcase/e2e-dashboard',
  custom_commands_path: path.resolve(rootPath, 'config/custom_commands'),
```

1. Add a new command in `package.json` to run it

   ```typescript
    "e2e-dashboard": "rimraf ./tests/e2e/dist && babel ./tests/e2e/src --out-dir ./tests/e2e/dist && npm run dev:e2e-dashboard",
    "dev:e2e-dashboard": "nightwatch --config nightwatch.config.dashboard.dev.js",
   ```

