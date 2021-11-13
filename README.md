# @walbay/react-web-config

[![npm version](https://badge.fury.io/js/%40walbay%2Freact-web-config.svg)](https://badge.fury.io/js/%40walbay%2Freact-web-config)

[react-native-config](https://github.com/luggit/react-native-config) for Web.
Config variables for React Native apps *and React Native Web apps*

Module to expose config variables to your javascript code in React Native, supporting both iOS and Android *and web*.

### Overview

[react-native-web](https://github.com/necolas/react-native-web) is a project to bring [react-native](https://github.com/facebook/react-native) to the web. [Read more](https://github.com/necolas/react-native-web#why).

`react-native-web` lets us to write a single app that runs on mobile platform, ie iOS and Android, as well as browser, however, a typical `react-native` project will use libraries such as `react-native-config` that works perfectly on `react-native` but not on `react-native-web`. `react-web-config` allows you to continue using `react-native-config` seamlessly on the web by adding a few lines in your webpack config.

### Usage

Step 1 and 2 is what you have done if you follow the [guides](https://github.com/luggit/react-native-config#usage) from react-native-config.


1) Create a new file `.env` in the root of your React Native app:

```js
// .env
SUPER_DUPER_API=https://superdupertrivia.com
SECRET_KEY=superdupersecret
```

2) Then access variables defined there from your app:

```js
  // app.js
  import Config from '@walbay/react-native-config'
  Config.SUPER_DUPER_API  // 'https://superdupertrivia.com'
```

However if you want to have Step 2 to work on a `react-native-web` project, you will need to configure the following in your `webpack.config.js`:

```diff
  // webpack.config.js

+ const ReactWebConfig = require('@superdupertrivia/react-web-config/lib/ReactWebConfig').ReactWebConfig;
+ const path = require('path');

+ const envFilePath = process.env.ENVFILE || path.resolve(__dirname, '.env');

  module.exports = {
    ...
    plugins: [
      ...
+     /* define __REACT_WEB_CONFIG__ */
+     ReactWebConfig(envFilePath)
    ],
    resolve: [
      alias: [
        ...
+       /* set alias from react-native-config to react-web-config */
+       'react-native-config': '@walbay/react-web-config',
        'react-native': 'react-native-web'
      ]
    ]
  }
```

### Contributors
- @tanhauhau (Original Author)
- @Hortau
- @walbay

### License

MIT
