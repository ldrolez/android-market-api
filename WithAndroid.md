## Authentication ##

To get a valid authsub token from an android device using the unofficial google clientlogin api for android (client.jar)

From http://www.toxicbakery.com/android-development/getting-google-auth-sub-tokens-in-your-android-applications/

```
<uses-permission android:name="android.permission.MANAGE_ACCOUNTS"></uses-permission>
<uses-permission android:name="android.permission.GET_ACCOUNTS"></uses-permission>
<uses-permission android:name="android.permission.USE_CREDENTIALS"></uses-permission>
<uses-permission android:name="android.permission.INTERNET"></uses-permission>
```

Not tested :

```
private String updateToken(boolean invalidateToken) {
    String authToken = "null";
    try {
        AccountManager am = AccountManager.get(context);
        Account[] accounts = am.getAccountsByType("com.google");
        AccountManagerFuture<Bundle> accountManagerFuture;
        if(activity == null){//this is used when calling from an interval thread
            accountManagerFuture = am.getAuthToken(accounts[0], "android", false, null, null);
        } else {
            accountManagerFuture = am.getAuthToken(accounts[0], "android", null, activity, null, null);
        }
        Bundle authTokenBundle = accountManagerFuture.getResult();
        authToken = authTokenBundle.getString(AccountManager.KEY_AUTHTOKEN).toString();
        if(invalidateToken) {
            am.invalidateAuthToken("com.google", authToken);
            authToken = updateToken(false);
        }
    } catch (Exception e) {
        e.printStackTrace();
    }
    return authToken;
}
```

## Locale and Operator ##

Quote from Aladin Q :

I noticed it is important to fill the "setLocale" and "setOperator" methods in order to expect "correct results" from market session (understand "correct results" as "similar results if the same query is made in the official Android Market application).

Per example, in order to avoid modifications of your sources and because "Orange F" is not listed, we can pass the results of the snippet below to the method "setOperator":


```
TelephonyManager mTelephonyManager = (TelephonyManager) getSystemService(TELEPHONY_SERVICE); 
 mTelephonyManager.getSimOperatorName(); 
 mTelephonyManager.getNetworkOperatorName(); 
 mTelephonyManager.getSimOperator() 
```