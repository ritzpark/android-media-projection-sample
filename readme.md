The purpose of this project is to do the Google's job when it comes to update their samples accordingly with their docs/releases.

We have an official MediaProjection sample available through the AndroidStudio indexer, but it doesn't show how to use it in the newer Android 14 (and its security mechanisms changes).

Enjoy it, because I spent almost two weeks gathering pieces from all over the places until I get this working :'|

**Here is a resume of what you need to do:**

1. Call the ```MediaProjectionManager::createScreenCaptureIntent()``` method to start the process.
2. Launch the retrieved intent and capture its result (code, data, etc).
3. If the build version is prior **Android 14**: just get the ```MediaProjection``` instance from the ```MediaProjectionManager``` service using the intent data and create the virtual display to start everything.
3.1 Otherwise, you need to **start a foreground service** to be able to use the feature and only after it started, you can get the ```MediaProjection``` instance (if you try it before, a *IllegalStateException* will be thrown).
4. (optional) In this sample, I show the result in the only activity available, so since I need access to its views, I used a ```BroadcastReceiver``` to communicate the activity the exact moment that the service started, to avoid race conditions.