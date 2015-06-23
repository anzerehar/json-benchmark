Correctness and Performance benchmark for various Java-based JSON libraries

# Which parser is fastest on Android? #

Here's a quick overview from the implementor of Android's two JSON parsers:
  * [org.json](http://developer.android.com/reference/org/json/JSONObject.html) The API requires you to load the entire document into a String. This is somewhat cumbersome to use and inefficient for large documents. But it's a DOM model so you can get a lot done with very little code.
  * [android.util.JsonReader](http://developer.android.com/reference/android/util/JsonReader.html) is a basic pull parser. It has a concise API and is reasonably efficient. It's included in Android 3.0. For earlier Android releases it's available as [google-gson-stream](http://code.google.com/p/google-gson/downloads/list) which offers the same API in a 14 KiB .jar file. The [larger GSON library](http://code.google.com/p/google-gson/) also offers a DOM API and easy databinding.
  * [Jackson](http://jackson.codehaus.org/) is efficient and fully-featured. Jackson has a capable but large API. It accomplishes great efficiency by going to some extremes, like implementing its own floating point parsing and charset decoding. If you use Jackson, you may want to use [ProGuard](http://developer.android.com/guide/developing/tools/proguard.html) to shrink its 222 KiB jar.

As for hard numbers, Jackson has the edge:
```
  16 Kb Google Reader data:
  JsonReader 2.3 MBps
  Jackson 3.8 MBps

  68 Kb Twitter data:
  JsonReader 2.2 MBps
  Jackson 5 MBps

  185 Kb Google Reader data:
  JsonReader 2.5 MBps
  Jackson 6.5 MBps
```

Some of the optimizations currently employed by Jackson may be coming to Android.