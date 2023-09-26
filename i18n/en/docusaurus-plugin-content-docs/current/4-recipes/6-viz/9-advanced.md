---
sidebar_position: 9
---

# Advanced Configs

The "Preferences" interface of the visualization page offers settings related to display, language, privacy, experimental features, and more.

## Set Display Language

Click on the "Preferences" icon in the bottom right corner of the visualization interface to open the preferences settings and make the necessary changes.

![viz-preferences-1](../img/viz-preferences-1.png)

## Adjust Preload Time Length and Single Request Time Length

> Please use this feature with caution, as it may lead to unexpected webpage lags or crashes.

### Key Term Explanation

- Preload Time Length: The amount of data loaded in advance from the current playback position, measured in seconds. The default is thirty seconds. Setting it too long might cause lags or even webpage crashes due to excessive memory usage.
- Single Request Time Length: The length of data requested from the server each time, measured in seconds. The default is five seconds. Setting it too long might cause increased server processing time or even request failures.

### Setting Method

- Press the `F12` key to open the developer tools.
  ![open-devtools](../img/open-devtools.png)
- In the developer tools, click on the `Application` tab, then the `Storage` tab, and then the website's URL.
  ![open-local-storage](../img/open-local-storage.png)
- At the bottom of `Local Storage`, double-click to add the `readAheadDuration` and `singleRequestTime` key-value pairs. These set the preload time length and single request time length, respectively, in seconds.
  ![set-readAheadDuration-and-singleRequestTime-value](../img/set-readAheadDuration-and-singleRequestTime-value.png)
- Refresh the page to apply the changes.

PS: If you have set these values before, you can directly modify the corresponding values in `Local Storage`.
