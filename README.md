# react-native-odde-alipay

React Native Module for alipay.com. This is a fork of react-native-yunpeng-alipay (I can't find a public repo of it, therefore start over with what I can get from npm). Although some new feature has been added on top of it, all honor should go to react-native-yunpeng-alipay.

## install

```
yarn add react-native-odde-alipay
```

## Android

### With react-native

```
react-native link react-native-odde-alipay
```

### Manually

* android/settings.gradle

```
include ':react-native-odde-alipay'
project(':react-native-odde-alipay').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-odde-alipay/android')
```

* android/app/build.gradle

```
dependencies {
    compile project(':react-native-odde-alipay')
}
```

* register module (in MainActivity.java)

```java
...

import com.odde.alipay.AlipayPackage; // <--- IMPORT

public class MainActivity extends ReactActivity {

    ...

    @Override
    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
            new MainReactPackage(),
            new AlipayPackage() // <--- ADD HERE
        );
    }
}
```

## iOS

### With react-native

```
react-native link react-native-odde-alipay
```

### Manually

> Link `AlipayModule` library from your `node_modules/react-native-odde-alipay/ios` folder like its [described here](http://facebook.github.io/react-native/docs/linking-libraries-ios.html). Don't forget to add it to "Build Phases" of project.

### Config

* Added the following libraries to your "Link Binary With Libraries":
  * [x] CoreMotion.framework
  * [x] CoreTelephony.framework
  * [x] libc++
  * [x] libz
  
* add `URL Schema` as your app id for `URL type` in `Targets - info`
* Make sure you have these code in AppDelegate.m to enable callback

```objective_c
#import "AlipayModule.h"
```

```objective_c
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
  [AlipayModule handleCallback:url];
  return YES;
}
```

### General Usage

```javascript
import Alipay from 'react-native-odde-alipay';

```

```javascript
Alipay.pay("signed pay info string").then(function(data){
                    console.log(data);
                }, function (err) {
                    console.log(err);
                });

```

### Use Alipay Sandbox (Android only)

```javascript
Alipay.useSandbox(true);

```

For more detail about sandbox, please refer to [this link](https://docs.open.alipay.com/200/105311).

