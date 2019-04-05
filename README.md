# firestorm-flatpak

Flatpak Builder files for allowing Firestorm Viewer to run as a Flatpak.

### Broken
* ~~32bit support (easy fix)~~
* CEF (setuid sandbox?) so no web views
* ~~gconf (setting secondlife:// handler)~~ fixed. using x-scheme-handler and gdbus instead.
* ~~Nvidia probably does not work.~~ It works! nVidia driver from Flathub must be installed (maybe preferable to use hosts instead?)
* Can't upload/download files outside of XDG directories (Documents etc).
* ~~launch_url.sh needs to be replaced with xdg-open~~ fixed

### Build & Install

```shell
sudo flatpak-builder --install --install-deps-from=flathub _build org.firestormviewer.FirestormViewer.json --force-clean
```

#### Notes
* $HOME is not allowed because Firestorm does not use $XDG_DATA_DIRS, and we bind mount ~/.firestorm_x64 => ~/.var/app/org.firestormviewer.FirestormViewer

    Gotta keep that home directory squeaky clean :D. A potential alternative to this is using portals.

* This does not build the viewer. Integrating Flatpak into the build process of the viewer is a lot more additional work but at least we can experiment with how Firestorm handles being inside modern Linux sandbox. 
* We kill the dependency issues that plague the Linux version of the viewer

GNOME now also monitors and manages our flatpak too.

![](https://i.imgur.com/m59sSOy.png)