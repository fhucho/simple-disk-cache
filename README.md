#### What is this?

This is an easy to use disk cache which uses [DiskLruCache](https://github.com/JakeWharton/DiskLruCache) under the hood. The DiskLruCache is nice, but it has too low level interface for most use cases. Besides the DiskLruCache, it also requires the [Apache Commons IO](http://commons.apache.org/proper/commons-io) lib (but it should be easy to remove this dependency).

#### Quick intro

1. Every cache entry has a value and metadata of type `Map<String, Serializable>`.
1. Any String can be used as cache key.
1. Open the cache with `SimpleDiskCache.open(dir, appVersion, capacityBytes)`. This cannot be called twice with the same dir, otherwise `RuntimeException` will be thrown mercilessly.
1. To put a String to the cache, call `cache.put(key, string, metadata)`. Or just `cache.put(key, string)`. That's up to you.
1. To put something else to the cache, get an `OutputStream` with `cache.openStream(key, metadata)`, write something to it and close it. The stream is buffered.
1. `getString(key)` returns `StringEntry` or `null`. `StringEntry` contains string and metadata. `getBitmap(key)` is the same but for bitmaps.
1. `getInputStream(key)` returns `InputStreamEntry`, which must be closed.
