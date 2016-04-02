---
layout: post
title: "Android Dev Best Practice"
---
### IntentService will create worker thread automatically for you
* Set ```android:exported="false"``` flag if the service is only used locally
* Broadcast could be used to notify back the caller, prefer [LocalBroadcastManager](http://developer.android.com/reference/android/support/v4/content/LocalBroadcastManager.html) to send broadcast

### Repack Android image
* ```ext2simg system.ext4 system.img.ext4```
