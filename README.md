# micro-lc-prerender
Prerender container for improving SEO of micro-lc components.

## Requirements

- Docker

## Usage

Pull and run the image:

```
docker pull microlc/micro-lc-prerender
docker run -p 3000:3000 microlc/micro-lc-prerender
```
Prerender will now be running on http://localhost:3000. Try the container out with curl:

```
curl http://localhost:3000/render?url=https://www.example.com/
```

## Prerender plugins

A few default plugins have been activated by default (see `server.js`):
- [blacklist](https://github.com/prerender/prerender/blob/master/lib/plugins/blacklist.js)
- [httpHeader](https://github.com/prerender/prerender/blob/master/lib/plugins/httpHeaders.js)
- [removeScriptTags](https://github.com/prerender/prerender/blob/master/lib/plugins/removeScriptTags.js)

This can be modified by creating your own `server.js` and mounting this file as a docker volume:

```
docker run -p 3000:3000 -v $(pwd)/server.js:/home/node/server.js microlc/micro-lc-prerender
```

## Prerender memory cache

The [prerender-memory-cache](https://github.com/prerender/prerender-memory-cache) plugin is not activated by default.
You can activate it with the environment variable `MEMORY_CACHE=1`.

You can customize cache behavior with environment variables :
- CACHE_MAXSIZE=1000 : max number of objects in cache
- CACHE_TTL=6000 : time to live in seconds

```
docker run -p 3000:3000 -e MEMORY_CACHE=1 -e CACHE_MAXSIZE=1000 -e CACHE_TTL=6000 microlc/micro-lc-prerender
```

## Prerender documentation

For further details, check out the official Prerender documentation: https://github.com/prerender/prerender
