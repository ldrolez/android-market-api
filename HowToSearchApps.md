
```
String query = "maps";
AppsRequest appsRequest = AppsRequest.newBuilder()
                                .setQuery(query)
                                .setStartIndex(0).setEntriesCount(10)
                                .setWithExtendedInfo(true)
                                .build();
                       
session.append(appsRequest, new Callback<AppsResponse>() {
         @Override
         public void onResult(ResponseContext context, AppsResponse response) {
                  // Your code here
                  // response.getApp(0).getCreator() ...
                  // see AppsResponse class definition for more infos
         }
});
```

This is what you can get from a search query :
```
{
  "app": [
    {
      "rating": "4.642857142857143",
      "title": "Ruboto IRB",
      "ratingsCount": 14,
      "creator": "Jan Berkel",
      "appType": "APPLICATION",
      "id": "9089465703133677000",
      "packageName": "org.jruby.ruboto.irb",
      "version": "0.1",
      "versionCode": 1,
      "creatorId": "\"Jan Berkel\"",
      "ExtendedInfo": {
        "category": "Tools",
        "permissionId": [
...
```

You can search by package using :
```
String query = "pname:<package>";
```

By developper name :
```
String query = "pub:<name>";
```

Check out the [Official Android Doc](http://developer.android.com/guide/publishing/publishing.html) (?q=xxxx)