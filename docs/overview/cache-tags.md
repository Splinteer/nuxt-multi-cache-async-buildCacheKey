# Cache Tags

Cache tags make cache invalidation easier, because they offer a way to identify
cached items.

## Basics

A cache tag is a unique identifier of an entity, like an article, an image or a
configuration. A few examples of what a cache tag might look like:

- `article:235`
- `language:de`
- `image:313`
- `config:site:page_title`
- `image_style:hero_large_retina`

Typically, cache tags are generated by a backend (e.g. Drupal, Laravel,
Symfony) and are provided to the frontend via a HTTP header. But they can also
be managed directly in your Nuxt app.

Usually a backend will trigger invalidations. For example when editing the
article with ID 235, it will perform the POST request to purge the article:235
tag in nuxt-multi-cache. Or when a German interface translation is edited it
will purge all cache items with the `language:de` tag.

## Integration

The component cache, data cache and route cache provide a way to store cache
tags along the cached item.

## Purging

The [API](/features/api) offers an endpoint to purge items by cache tag. In
addition you can inspect the cache tags for each item.

### Example: Caching search result pages

You could cache ElasticSearch search result pages using a single tag:
search_page. Now whenever you reindex your data, you afterwards issue a purge
request for that tag via cURL.