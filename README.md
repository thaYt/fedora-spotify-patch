# fedora linux spotify patcher
## for when [the normal repo](https://www.github.com/rpmfusion/lpf-spotify-client) is outdated

---

### a semi-automatic script for this is also included [here](https://www.github.com/thaYt/fedora-spotify-patch/blob/master/fsp), you will still need to edit the spec file when it asks you and remove a line

## to install spotify:
### dependencies:
to install dependencies, run these two commands:
```shell
sudo dnf copr enable patrickl/libcurl-gnutls -y
sudo dnf install alien rpmrebuild rpmdevtools libcurl-gnutls -y
```
spotify **will not run** if you don't install the Copr repo (at least for me)

### installation:
first download the most recent .deb release [here](https://repository.spotify.com/pool/non-free/s/spotify-client/)

then convert it to a .rpm file:
```shell
sudo alien -rcv ./spotify-client_*.deb
```

rebuild the rpm to remove a dependency error, remove the line `%dir %attr(0755, root, root) "/usr/bin"`
```shell
EDITOR=nano rpmrebuild -d . -ep ./spotify-client-*.rpm
```

and you're done! you should have a working .rpm file in ./x86_64/

use this command to install it:
```shell
sudo dnf localinstall ./x86_64/spotify-client-*.rpm
```
