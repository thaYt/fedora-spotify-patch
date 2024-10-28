# Fedora linux spotify installer
## for when [the normal repo](https://www.github.com/rpmfusion/lpf-spotify-client) is outdated

### an automatic script for this is included [here](https://www.github.com/thaYt/fedora-spotify-patch/blob/master/fsp)
```
wget https://github.com/thaYt/fedora-spotify-patch/blob/main/fsp
chmod +x fsp
sudo ./fsp install
```

## manual installation:

### dependencies:
please install these: `alien rpmrebuild rpmdevtools`

first download the most recent .deb release [here](https://repository.spotify.com/pool/non-free/s/spotify-client/)

then convert it to a .rpm file:
```shell
sudo alien -rcv ./spotify-client_*.deb
```

rebuild the rpm to remove a dependency error
```shell
rpmrebuild -d . -ep ./spotify-client-*.rpm
```
remove the line 

```%dir %attr(0755, root, root) "/usr/bin"```

and you're done! you should have a working .rpm file in ./x86_64/

finally, install it:
```shell
sudo dnf localinstall ./x86_64/spotify-client-*.rpm
```
