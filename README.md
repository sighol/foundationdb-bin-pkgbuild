This package contains foundationdb binaries for both the server and the client.

This package was created because the foundationdb AUR packages was based on the
DEB packages and weren't using systemd.

After installation, remember to configure a database. For example, using

```bash
fdbcli --exec configure new single memory
```
This is only needed once, and could probably be added to the installation script.
