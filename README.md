# memcached

[Memcached](https://memcached.org) template for Runway. Simple, fast,
multi-threaded in-memory key-value cache.

Single instance. Nothing is kept on disk: a restart empties the cache.

## Deploy

WIP

## Inputs

| Input | Default | Notes |
| --- | --- | --- |
| `image_tag` | `1.6.45-alpine` | Alpine or Debian (trixie) base |
| `memory_mb` | `64` | Cache size. Keep it well below the plan's RAM |
| `max_connections` | `1024` | Max open client connections |

## Outputs

`DSN`

## Connecting

Not routed — reachable only from inside your organization's network, at:

```
<app>.<app>.svc.cluster.local:11211
```

`<app>` is your app name. There is no login.

## Notes

- **No auth.** Memcached has no simple password option, so the template does
  not publish a route. Any app in your network can read and write.
- **No persistence.** Use it as a cache only. For data you must keep, use
  Valkey.
- **Size the cache to the plan.** The free plan has 128 MB RAM; the default
  64 MB leaves room for connections and overhead. On bigger plans, raise
  `memory_mb`.
- UDP is off.

## License

Memcached is BSD-3-Clause. This template is maintained by Runway.
