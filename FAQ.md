## Server return a 400 Bad Request ##

  * Some request parameters are incorrect. For example you can't query more than 10 results par request. If you try to setResultCount(11), you'll get a HTTP 400 Error.

  * You are doing to many request, try putting some Thread.sleep and check if the problem persist.

entriescount must be less or equals 10
to fetch a list of entries, you have to do multiple queries :
  * startIndex=0, count=10
  * startIndex=10, count=10
  * startIndex=20, count=10
  * ...

## How can i download the app ? ##

Not supported for now, shouldn't be too hard, feel free to contribute if you can

## App missing in the search result ##

Some users reported that you have to set the android Id to see copy protected apps. See google groups about this topic.

## How can i get the whole list of apps ##

Looks like google is trying to prevent this :
  * startIndex cannot be over 800 or so
  * resultCount cannot be over 10
  * if you do too many request, you'll get HTTP 400 error. This is a google market server protection, there is nothing this library can do about it : use multiple google accounts with multiple IP

## My question is not in this list ##

Post it HERE http://groups.google.com/group/android-market-api