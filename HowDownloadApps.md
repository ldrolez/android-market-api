The service to use for login during apps download must be **androidsecure**, otherwise **android** (e.g. to get apps info). To use androidsecure, the input param for MarketSession constructor must be true!
Step to download apps:
  1. Create a new session for the androidsecure service and login
```
  MarketSession session = new MarketSession(true);

        System.out.println("Login...");
        session.login(login,password, androidId);
```
  1. Issue a GetAssetRequest for the specifed assetId (application identifier in the market)
```
        InstallAsset ia = session.queryGetAssetRequest(assetId).getInstallAsset(0);
        String cookieName = ia.getDownloadAuthCookieName();
        String cookieValue = ia.getDownloadAuthCookieValue();
```
  1. Retrieve the blob containg the url for the required assetId
```
        URL url = new URL(ia.getBlobUrl());

        HttpURLConnection conn = (HttpURLConnection)url.openConnection();
        conn.setRequestMethod("GET");
        conn.setRequestProperty("User-Agent", "Android-Market/2 (sapphire PLAT-RC33); gzip");
        conn.setRequestProperty("Cookie", cookieName + "=" + cookieValue);
```
  1. Save the stream onto filesystem
```
        InputStream inputstream =  (InputStream) conn.getInputStream();
        String fileToSave = assetId + ".apk";
        System.out.println("Downloading " + fileToSave);
        BufferedOutputStream stream = new BufferedOutputStream(new FileOutputStream(fileToSave));
        byte buf[] = new byte[1024];
        int k = 0;
        for(long l = 0L; (k = inputstream.read(buf)) != -1; l += k )
            stream.write(buf, 0, k);
        inputstream.close();
        stream.close();  
```