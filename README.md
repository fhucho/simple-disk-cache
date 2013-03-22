# What is this?

This is an easy to use disk cache which uses [DiskLruCache](https://github.com/JakeWharton/DiskLruCache) under the hood. The DiskLruCache is nice, but it has a too low level interface for most use cases. Besides the DiskLruCache, it also requires the [Apache Commons IO](http://commons.apache.org/proper/commons-io) lib (but it should be easy to remove this dependency).

Quick intro:

1. Every cache entry has a value and Map<String, Serializable> metadata.
2. Any String can be used as cache key.
3. Open the cache with `SimpleDiskCache.open(dir, appVersion, capacityBytes)`. This can't be called twice with the same dir, otherwise a RuntimeException will be thrown mercilessly.
4 Any String can be used as a cache key.
5. To put a String to the cache, call `cache.put(key, string, metadata)`. Or just `cache.put(key, string)`. That's up to you.
6. InputStream can be put similarly, but don't forget to close it.
7. You can also do `OutputStream os = cache.openStream(key, metadata)`, write something to the stream and close it. The stream is buffered.
8. `getString(key)` returns StringEntry or null. StringEntry contains String and metadata. `getBitmap(key)` is similar. `getInputStream(key)` is also similar but it must be closed.
