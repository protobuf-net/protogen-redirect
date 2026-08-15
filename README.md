# protogen redirect

Nothing but redirects. This repo exists so that `protogen.marcgravell.com` — the old home of the
protogen tool — sends visitors to its new home at **[protobuf-net.dev](https://protobuf-net.dev)**.

| Old URL | New URL |
| --- | --- |
| `/` | `https://protobuf-net.dev/#schema` |
| `/decode` | `https://protobuf-net.dev/#decode` |
| anything else | `https://protobuf-net.dev/` (via `404.html`) |

The old site used real paths; the new one uses hash routing, hence the mapping.

## Why a repo rather than GoDaddy forwarding

GoDaddy does offer subdomain forwarding, but it does not serve HTTPS on the forwarded name — its
forwarding servers hold no certificate for the domain. The old site ran under `[RequireHttps]`, so
the links and bookmarks in the wild are all `https://`, and every one of them would hit a
certificate warning.

GitHub Pages issues a valid certificate for the custom domain, so this route actually works over
HTTPS. The trade-off is that these are client-side redirects rather than HTTP 301s, which carry
less weight with search engines. For a developer tool reached mostly by bookmark and README link,
that is the better trade.

If a true 301 is ever wanted, put Cloudflare (or similar) in front of `marcgravell.com` and use a
redirect rule instead — then this repo can be deleted.

## Setup

1. DNS at GoDaddy: `CNAME  protogen  protobuf-net.github.io.` — a plain DNS record, **not**
   GoDaddy's "Forwarding" feature.
2. Repo settings → Pages → source `main`, custom domain `protogen.marcgravell.com`, enforce HTTPS
   once the certificate is issued.
