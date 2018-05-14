# Android For Dummies That Know iOS

Just trying to keep some concepts straight in my 🧠 as I learn Android development.

(Was going to call it "Android By Andres" because that just rolls off the tongue.)

## App Config

### iOS

`Info.plist`

### Android

`AndroidManifest.xml`
Components.
App requirements (devices, min sdk version, etc...)

## App Resources

### iOS

`.xcassets`

### Android

`res/` directory.

## View Layout

### iOS

`.xib`/`.storyboard` files.

### Android

Each file has a `.xml` layout file where components are identified by `id`. This `id` is used to index into the `R.layout` object to access them in the code.

## View Objects

### iOS

`UIViewControllers`/`UIViews`

### Android

`Activities` are the VCs _"A single screen with a UI"_. They need to be added to the manifest file.

They are shown from other `Activities` via `Intents`. Example:

```java
Intent intent = new Intent(this /* the shower */, ShowedActivity.class /* the showee */);
intent.putExtra(EXTRA_KEY, "foo"); // passing data to the showee
startActivity(intent);
// startActivityForResult() (when you want the activity to return a result).
```

Intent-filters can be used to let the system pick out the target automatically. Useful for cross-app communications. Example:

```java
// Create the text message with a string
Intent sendIntent = new Intent(); // note there are no params
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.setType("text/plain");
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
// Start the activity
startActivity(sendIntent);
```

**Intent message is asynchronous.**

## View Lifecycle

|iOS|Android|
|---|-------|
|viewDidLoad|onCreate()|
|viewWillAppear|onStart() (onRestart())|
|viewDidAppear|onResume()|
|viewWillDisappear|onPause()|
|viewDidDisappear|onStop()|
|old unload|onDestroy()|

When launching an activity from another, this is the flow:

```text
Home-Activity::onPause()
Target-Activity::onCreate()
Target-Activity::onStart()
Target-Activity::onResume()
Home-Activity::onStop()
```

## TODO

Other "App Components":

- Services
- Broadcast receivers
- Content providers
