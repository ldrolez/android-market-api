
```
 CommentsRequest commentsRequest = CommentsRequest.newBuilder()
                                .setAppId("7065399193137006744")
                                .setStartIndex(0)
                                .setEntriesCount(10)
                                .build();
          
 session.append(commentsRequest, new Callback<CommentsResponse>() {
  @Override
    public void onResult(ResponseContext context, CommentsResponse response) {
        System.out.println("Response : " + response);
        // response.getComments(0).getAuthorName()
        // response.getComments(0).getCreationTime()
        // ...
    }
});

session.flush();
```

Sample response :

```
{
  "comments": [
    {
      "rating": 5,
      "creationTime": 1269710736815,
      "authorName": "Nate Kidwell",
      "text": "Tremendous application. More examples would be great (as would integrated rubydocs), but awesome all the same.",
      "authorId": "04441815096871118032"
    },
...
```