# Prowlarr for Ciniva

Prowlarr image used by the [Ciniva](https://github.com/Ciniva/ciniva) downloads stack: a pinned, checksum-verified
release running as an unprivileged user (1000:1000) with a read-only root filesystem. In-app updates are disabled;
updating means bumping the pinned version here.

Published to `ghcr.io/ciniva/prowlarr` by GitHub Actions for `vX.Y.Z` tags (`X.Y.Z`, `latest`, `sha-<short>`); run the
workflow by hand to publish any branch as `sha-<short>`.

```yaml
prowlarr:
  image: ghcr.io/ciniva/prowlarr:latest
  user: "1000:1000"
  read_only: true
  cap_drop: [ALL]
  security_opt: [no-new-privileges:true]
  volumes:
    - ./prowlarr:/config
  tmpfs:
    - /tmp:size=64m,mode=1777
  ports:
    - "9696:9696"
```

Prowlarr asks for a login on first visit. With the Ciniva qBittorrent plugin, put the API key in a secret file and pass
it as `PROWLARR_API_KEY_FILE`.
