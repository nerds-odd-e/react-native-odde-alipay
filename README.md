# react-native-odde-alipay

React Native Module for alipay.com. This is a fork of react-native-yunpeng-alipay (I can't find a public repo of it, therefore start over with what I can get from npm). Although some new feature has been added on top of it, all honor should go to react-native-yunpeng-alipay.

## Install

```
yarn add react-native-odde-alipay

react-native link react-native-odde-alipay
```

## Android Additional config

Add the following activity and permission config to `AndroidManifest.xml`:

```
<activity
  android:name="com.alipay.sdk.app.H5PayActivity"
  android:configChanges="orientation|keyboardHidden|navigation"
  android:exported="false"
  android:screenOrientation="behind" >
</activity>
<activity
  android:name="com.alipay.sdk.auth.AuthActivity"
  android:configChanges="orientation|keyboardHidden|navigation"
  android:exported="false"
  android:screenOrientation="behind" >
 </activity>
```

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

## iOS Additional config

Added the following libraries to your "Link Binary With Libraries":
* CoreMotion.framework
* CoreTelephony.framework
* libc++
* libz

Add `URL Schema` as your app id for `URL type` in `info.plist`

![](http://img.blog.csdn.net/20161116154414431)

Make sure you have these code in `AppDelegate.m` to enable callback

```objective_c
#import "AlipayModule.h"
- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication annotation:(id)annotation
{
  [AlipayModule handleCallback:url];
  return YES;
}
```

### General Usage

```
import Alipay from 'react-native-odde-alipay';
```

```
Alipay.pay("signed pay info string").then(function(data){
                    console.log(data);
                }, function (err) {
                    console.log(err);
                });
```

### Use Alipay Sandbox (Android only)

```
Alipay.useSandbox(true);
```

For more detail about sandbox, please refer to [this link](https://docs.open.alipay.com/200/105311).

