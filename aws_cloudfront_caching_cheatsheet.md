# CloudFront Cache TTL: Default TTL vs. Max TTL

In Amazon CloudFront, the **TTL (Time to Live)** determines how long cached content is considered fresh before CloudFront checks the origin server for an updated version. There are two primary TTL settings in CloudFront: the **Default TTL** and the **Maximum TTL**.

## Default TTL
- **Definition**: The Default TTL is the duration that CloudFront uses to cache an object before checking the origin server for a new version (if no other TTL headers are specified).
- **Default Value**: The default TTL is **86400 seconds** (24 hours). This is the period CloudFront will keep the content cached unless overridden by Cache-Control headers (e.g., `max-age` or `s-maxage`).
- **Customization**: You can configure the Default TTL on a per-distribution or per-cache behavior basis within the CloudFront settings.

## Maximum TTL (Max TTL)
- **Definition**: The Maximum TTL is the maximum time CloudFront will cache an object, regardless of any cache headers sent by the origin. If the cache control headers sent by the origin specify a TTL longer than the Max TTL, CloudFront will use the Max TTL instead.
- **Maximum Value**: The Maximum TTL you can set in CloudFront is **31536000 seconds** (1 year). This means that even if the origin specifies a longer TTL, CloudFront will not cache the object for more than one year.
- **Customization**: You can configure the Maximum TTL to control how long content is cached across all CloudFront edge locations.

## Key Differences
- **Default TTL**: This is the starting TTL value for cached content unless overridden by cache-control headers or other settings.
- **Max TTL**: This is the upper limit that CloudFront will apply, preventing the cache from holding content for longer than the specified maximum duration, even if the origin suggests a longer cache duration.

In summary:
- **Default TTL** (86400 seconds / 24 hours) determines how long CloudFront caches content by default unless overridden by the origin headers.
- **Max TTL** (31536000 seconds / 1 year) sets the maximum period that CloudFront will cache content, regardless of the cache headers provided by the origin.


# Overview of Caching Headers

Caching headers are HTTP headers used to control the caching behavior of responses from a server. They help optimize performance by reducing unnecessary requests and ensuring that clients (like browsers or intermediate caches) store and reuse resources effectively. Here is an overview of the most commonly used caching headers:

## 1. Cache-Control
- **Purpose**: This is the most important header for controlling cache behavior in modern HTTP applications. It provides directives to both browsers and intermediate caches (like CDNs).
- **Common Directives**:
    - **`no-cache`**: Instructs the cache to revalidate the resource with the server before using it, ensuring it is up to date.
    - **`no-store`**: Indicates that the resource should not be stored in the cache at all, ensuring it is always fetched from the server.
    - **`public`**: Marks the response as cacheable by any cache, even if it is associated with a private user.
    - **`private`**: Marks the response as cacheable only by the user's browser (not shared caches like CDNs).
    - **`max-age`**: Specifies the maximum time (in seconds) a resource is considered fresh. After this time, the cache will have to revalidate it.
    - **`s-maxage`**: Similar to `max-age`, but only applies to shared caches (like CDNs).
    - **`must-revalidate`**: Once the resource becomes stale (exceeds `max-age`), the cache must revalidate it with the server before using it.
    - **`proxy-revalidate`**: Instructs shared caches to revalidate the resource once it is stale, similar to `must-revalidate` but specifically for shared caches.

## 2. Expires
- **Purpose**: This header specifies a specific date and time after which the cached response is considered stale. It is a more traditional caching header and is now often used in combination with `Cache-Control`.
- **Usage**: If the `Cache-Control` header provides `max-age`, the `Expires` header is typically ignored unless the `Cache-Control` does not specify any expiration rules.
- **Value**: The value is usually a timestamp indicating when the cache expires.

## 3. ETag
- **Purpose**: The `ETag` header is a unique identifier assigned to a specific version of a resource. It is typically used for cache validation.
- **Usage**: When a client has a cached resource, it sends the `ETag` value in the `If-None-Match` header in subsequent requests. The server then compares this value with the current version of the resource. If they match, the server can return a `304 Not Modified` status, indicating that the cached resource is still valid.
- **Value**: Typically a hash or version string generated based on the content of the resource.

## 4. Last-Modified
- **Purpose**: The `Last-Modified` header indicates the date and time when the resource was last modified. It can be used to determine if the cached version is still valid by comparing it to the current version.
- **Usage**: When a client has a cached resource, it can send the `Last-Modified` value in the `If-Modified-Since` header with its next request. The server will compare this date to the resource's current modification date and respond with a `304 Not Modified` if the resource has not changed.
- **Value**: A date-time value that represents the last time the resource was modified.

## 5. Vary
- **Purpose**: The `Vary` header tells caches to store different versions of a resource based on the value of specific request headers. It ensures that caches differentiate responses based on factors like the `User-Agent`, `Accept-Encoding`, or other headers.
- **Usage**: For example, if the `Vary` header is set to `Accept-Encoding`, caches will store separate versions of the resource for different encodings (such as gzip or plain).
- **Value**: A comma-separated list of request headers that the cache should consider when deciding whether to serve a cached response.

## 6. Pragma
- **Purpose**: The `Pragma` header is an older HTTP/1.0 header that is still used for backward compatibility. It is mostly used with the `no-cache` directive to prevent caching in legacy browsers.
- **Usage**: While `Cache-Control` is preferred in modern HTTP/1.1, `Pragma` can still be used as a fallback in older HTTP versions or in specific scenarios.
- **Value**: Typically, the value is `no-cache`, indicating that caching is not allowed.

## 7. Age
- **Purpose**: The `Age` header provides the time in seconds since the resource was stored in the cache. It is useful for intermediate caches (like CDNs or proxies) to inform the client how long the resource has been cached.
- **Usage**: When a response is served from a cache, the `Age` header indicates how fresh it is.
- **Value**: A numeric value representing the age of the cached resource in seconds.

## 8. Cache-Control: immutable
- **Purpose**: This directive is used to indicate that a resource will not change over time, so there is no need for revalidation. It is typically used for static resources like images or versioned files.
- **Usage**: The `immutable` directive prevents browsers from checking if the resource has changed, assuming it will always be the same.
- **Value**: `immutable`

## 9. Content-Disposition
- **Purpose**: While not directly a caching header, `Content-Disposition` can impact caching behavior by specifying how the resource should be handled (e.g., as an attachment for download).
- **Usage**: If a resource is intended for download (e.g., a PDF file), the `Content-Disposition` header can indicate this, affecting whether or not it should be cached.
- **Value**: Can be set to `inline` or `attachment`, depending on the intended behavior.

## Conclusion
Caching headers are an essential part of web performance optimization, controlling how resources are stored, revalidated, and shared between the client and caches. By setting these headers appropriately, you can ensure that your web application performs efficiently while maintaining consistency and freshness of content. Understanding how and when to use each header, along with the nuances of cache control mechanisms, helps in balancing user experience with server load reduction.
