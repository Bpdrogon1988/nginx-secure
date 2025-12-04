# 🔒 nginx-secure

A hardened NGINX container image with a signed supply chain.

## Key hardening features
- ✅ Runs as the unprivileged `nginx` user listening on port **8080**
- ✅ Custom configuration with strict security headers (CSP, HSTS, COOP/COEP, CORP, Referrer-Policy, X-Permitted-Cross-Domain-Policies, X-Download-Options, X-Robots-Tag)
- ✅ Limits request methods to `GET`/`HEAD` and constrains buffer + body sizes
- ✅ Denies access to dotfiles while caching immutable assets efficiently
- ✅ Static assets shipped with Subresource Integrity (SRI) hashes
- ✅ Healthcheck verifies the container continues to serve traffic

## Build locally
```bash
docker build -t nginx-secure .
```

## Run the container
```bash
docker run --rm -p 8080:8080 nginx-secure
```

When running behind TLS termination, the container will emit HSTS headers. If you do not terminate TLS in front of this container, you should remove or adjust the `Strict-Transport-Security` header in `conf.d/default.conf`.

## Verify published image signature
```bash
cosign verify docker.io/brandenp88/nginx-secure:latest
```
