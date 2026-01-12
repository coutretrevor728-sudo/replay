/* eslint-disable no-undef */
const view = await chrome.devtools.recorder.createView(
  /* name= */ 'CoffeeTest',
  /* pagePath= */ 'Replay.html'
);

let latestRecording;

view.onShown.addListener(() => {
  // Recorder has shown the view. Send additional data to the view if needed.
  chrome.runtime.sendMessage(JSON.stringify(latestRecording));
});

view.onHidden.addListener(() => {
  // Recorder has hidden the view.
});

export class RecorderPlugin {
  replay(recording) {
    // Share the data with the view.
    latestRecording = recording;
    // Request to show the view.
    view.show();
  }
}

/* eslint-disable no-undef */
chrome.devtools.recorder.registerRecorderExtensionPlugin(
  new RecorderPlugin(),
  /* name=*/ 'CoffeeTest'
);# TestServer

This test server is used internally by Puppeteer to test Puppeteer itself.

### Example

```js
const {TestServer} = require('@pptr/testserver');

(async(() => {
  const httpServer = await TestServer.create(__dirname, 8000),
  const httpsServer = await TestServer.createHTTPS(__dirname, 8001)
  httpServer.setRoute('/hello', (req, res) => {
    res.end('Hello, world!');
  });
  console.log('HTTP and HTTPS servers are running!');
})();
```
