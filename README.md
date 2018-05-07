# Android For Dummies That Know iOS

Just trying to keep some concepts straight in my 🧠 as I learn Android development.

## View Layout

### iOS

`.xib`/`.storyboard` files.

### Android

Each file has a `.xml` layout file where components are identified by `id`. This `id` is used to index into the `R.layout` object to access them in the code.

## View Objects

### iOS

`UIViewControllers`/`UIViews`

### Android

`Activities` are shown from other `Activities` via `Intents`. Example:

```java
Intent intent = new Intent(this /* the shower */, ShowedActivity.class /* the showee */);
intent.putExtra(EXTRA_KEY, "foo"); // passing data to the showee
startActivity(intent);
```
