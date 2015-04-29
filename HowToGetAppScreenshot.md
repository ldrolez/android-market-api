
```

 GetImageRequest imgReq = GetImageRequest.newBuilder().setAppId("-7934792861962808905")
                                .setImageUsage(AppImageUsage.SCREENSHOT)
                                .setImageId("1")
                                .build();
   
session.append(imgReq, new Callback<GetImageResponse>() {
                                
                                @Override
                                public void onResult(ResponseContext context, GetImageResponse response) {
                                        try {
                                                FileOutputStream fos = new FileOutputStream("icon.png");
                                                fos.write(response.getImageData().toByteArray());
                                                fos.close();
                                        } catch(Exception ex) {
                                                ex.printStackTrace();
                                        }
                                }
});
session.flush();
                     
```