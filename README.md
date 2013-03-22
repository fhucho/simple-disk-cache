### What is this?

This is an easy to use disk cache which uses [DiskLruCache](https://github.com/JakeWharton/DiskLruCache) under the hood. The DiskLruCache is nice, but it has too low level interface for most use cases. Besides the DiskLruCache, it also requires the [Apache Commons IO](http://commons.apache.org/proper/commons-io) lib (but it should be easy to remove this dependency).

### Quick intro

Every cache entry has a value and metadata, the metadata are representad as `Map<String, Serializable>`. Any string can be used as a cache key.

##### Open

Open the cache with `SimpleDiskCache.open(dir, appVersion, capacityBytes)`. This cannot be called twice with the same dir, otherwise `RuntimeException` will be thrown mercilessly.

##### Put

To put a String to the cache, call `cache.put(key, string, metadata)`. Or just `cache.put(key, string)`. That's up to you.

To pour the content of an InputStream to the cache, just call `cache.put(key, inputStream, metadata)`. Don't forget to close the stream.

To put something else to the cache, call `cache.openStream(key, metadata)` to get an `OutputStream`, write something to it and close it. The stream is buffered.

##### Get

`cache.getString(key)` returns `StringEntry` or `null`. `StringEntry` contains string and metadata. For bitmaps, use `cache.getBitmap(key)`.

Use `cache.getInputStream(key)` to get an `InputStreamEntry` and close it when you're done please.
