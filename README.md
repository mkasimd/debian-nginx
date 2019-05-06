
Documentation is available on [nginx](http://nginx.org)

To add additional modules, put the modules into the directory `modules` and change the compiler flags in `debian/rules` and update possible dependencies under `debian/control` accordingly.
Be reminded that this source assumes that the the `rules` and especially the modules are located in `/usr/local/src/nginx/nginx-1-16.0/`, 
thus you might have to change the compiler flags according to your file path.

If you want to confugure nginx with ipscrub, you'll require [libbsd](https://libbsd.freedesktop.org/wiki/). Run `apt-get install libbsd-dev` to install it.
But the dependencies of the single packages are already set properly, so this shouldn't be a problem.

The releases already include debian packages (.deb file) while binaries ending with `full` include all modules (requires libbsd), `noSP` include all modules **except** `ngx_pagespeed` and the other binary including only the `ngx_headers_more` module. The dependencies are set properly while all releases depend on Openssl (≥ 1.1.1b).
