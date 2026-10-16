# sendmanagers-listmonk

Sendmanagers runs [listmonk](https://github.com/knadh/listmonk) **v6.2.0**,
unmodified, from the official `listmonk/listmonk` Docker image. listmonk is
free software under the GNU Affero General Public License v3.

The only files that differ from upstream are the ones in this repository. They
are loaded at runtime with listmonk's documented `--static-dir` option
(`LISTMONK_static_dir`), which lays them over the built-in files:

| File | Replaces upstream | What changed |
| --- | --- | --- |
| `static/email-templates/subscriber-optin.html` | [`static/email-templates/subscriber-optin.html`](https://github.com/knadh/listmonk/blob/v6.2.0/static/email-templates/subscriber-optin.html) | The double opt-in confirmation mail follows the subscriber's language (`attribs.taal`: nl, fr, en, de, es, it) for both body and subject, and shows the sender's logo instead of the instance logo. |

Every other file is exactly as published upstream at the tag `v6.2.0`.

## Running it yourself

```yaml
services:
  listmonk:
    image: listmonk/listmonk:v6.2.0
    environment:
      LISTMONK_static_dir: /listmonk/sd-static
    volumes:
      - ./static:/listmonk/sd-static:ro
```

The logo is requested from `<root_url>/merk/<workspace>/logo`, a route that
Sendmanagers' own proxy serves; without that proxy the image is simply absent.

## License

GNU Affero General Public License v3, the same as listmonk — see `LICENSE`.
