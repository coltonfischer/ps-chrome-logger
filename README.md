
# PS-Chrome-Logger

A utility to allow PeopleSoft developers to write log statements to the Chrome browser console from PeopleCode.

### Dependencies

- You must be on PeopleTools `8.55` or later.

- [Optional] Install the [PS-Jsonify](https://github.com/coltonfischer/ps-jsonify) utility to enable logging of PeopleCode object types such as Arrays, App Classes, Records, and Rowsets with one line of code.

### Installing

- Download and import the [PeopleSoft project](https://github.com/coltonfischer/ps-chrome-logger/raw/master/PSM_CHROME_LOGGER.zip) into App Designer.

- Install the [Chrome Logger extension](https://chrome.google.com/webstore/detail/chromephp/noaneddfkdjfnfdakjjmocngnfkfehhd) for Google Chrome.

- Click the extension icon to enable logging for the current tab's domain (It will light up blue).

> ![Toggle Chrome Logger](https://craig.global.ssl.fastly.net/img/chromelogger/toggle.gif)

### Usage

You can to write log statements from PeopleCode like this:

```java
(CreateObject("L:O")).G("Hello from the server");
```

The log output will show in the Chrome browser console like this:

> ![Log String Output](https://github.com/coltonfischer/ps-chrome-logger/raw/master/examples/Output_String.png)

If you have the PS-Jsonify utility installed then you can output PeopleCode object types.  Here is an example statement logging the Landing Page Rowset from the `PT_LANDINGPAGE` Component PeopleCode:

```java
Local  Rowset  &rsLandingPages = GetLevel0()(1).GetRowset(Scroll.PTNUI_LP_PAGE);

(CreateObject("L:O")).G(&rsLandingPages);
```

The log output will show in the Chrome browser console like this:

> ![Log Rowset Output](https://github.com/coltonfischer/ps-chrome-logger/raw/master/examples/Output_Rowset.png)

If you do not use the PS-Jsonify utility then above example would output "Rowset".

### Limitations

- This utility only supports the output of log statements to the Chrome browser console in PeopleCode contexts where the `%Response` object is available.  You can extend the [logging facade class](https://github.com/coltonfischer/ps-chrome-logger/blob/master/src/PeopleCode/Application%20Packages/L/O.pcode) to use different logging strategies in contexts where the `%Response` object is unavailable.  An example might include writing to a file when in an Integration Broker or Process Scheduler context.

- This utility communicates log data via HTTP response headers. The Chrome browser has a [limit of 250kb](https://stackoverflow.com/questions/3326210/can-http-headers-be-too-big-for-browsers) across all headers for a single request so this poses a limit on the amount of data you can log.

### Additional Details

Blog Post: [Server Side Logs in the Browser Console](https://www.peoplesoftmods.com/utilities/ps-chrome-logger/)
