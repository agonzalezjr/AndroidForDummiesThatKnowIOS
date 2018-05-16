# Android For Dummies That Know iOS

Just trying to keep some concepts straight in my 🧠 as I learn Android development.

(Was going to call it "Android By Andres" because that just rolls off the tongue.)

This is the best landing page I have found so far for introductions: https://www.raywenderlich.com/category/android

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

## Composition

### iOS

Nested View Controllers

### Android

Fragments

## Lists

### iOS

`UITableViewController` displays a `UITableView` (and it uses a `UITableViewDataSource` and `UITableViewDelegate`)

### Android

_OLD:_ No recycling: `Activity` displays `ListView` (and it uses an `Adapter` (both data source and cell view provider))

_NEW:_ Recycling: `Activity` displays `RecyclerView` (it uses an `Adapter`, a `ViewHolder`, and a `LayoutManager`)

- When implementing the `Adapter`:
  - Use a subclass of `RecyclerView.Adapter<ViewHolder>`
  - Implement your `ViewHolder` (usually a nested class of the `Adapter`)
    - `onCreateViewHolder` called when there aren't view holders available to recycle. Note there is no "position" here at all
    - `onBindViewHolder` called when a new item will be available on screen for a specific position and the holder needs some data
- Item selection is responsibility of each item/view instead of the recycler view
  - However, the recycler view can have attached an `ItemTouchHelper` to handle swipe/move gestures on each item

## TODO

- Services
- Broadcast receivers
- Content providers (Cursors?)
- Screen sizes and pixel densities
- ActionBar buttons/menus and overflows
- Dialog vs Toast vs Popups