
Documentation is available on [nginx](http://nginx.org)

To add additional modules, put the modules into the directory `modules`, change the compiler flags in `debian/rules` and update possible dependencies under `debian/control` accordingly.
Be reminded that this source assumes that the the `rules` and especially the modules are located in `/usr/local/src/debian-nginx/`, 
thus you might have to change the compiler flags according to your file path.

If you want to confugure nginx with ipscrub, you'll require [libbsd](https://libbsd.freedesktop.org/wiki/). Run `apt-get install libbsd-dev` to install it.
But the dependencies of the single packages are already set properly, so this shouldn't be a problem.

The releases already include debian packages (.deb file); for more information on the specific packages, see the releases section. The dependencies are set properly while all releases depend on Openssl (≥ 1.1.1b).

To use the zstd compression module, compile the zstd library first. To do so, the [zstd-nginx-module](https://github.com/mkasimd/zstd-nginx-module) has the [zstd](https://github.com/facebook/zstd) submodule included. Just run the following commands on your CLI to compile and install the zstd library:

```sh
$ cd modules/zstd-nginx-module/zstd
$ make install
```
