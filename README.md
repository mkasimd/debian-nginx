
Documentation is available on [nginx](http://nginx.org)

To add additional modules, put the modules into the directory `modules` and change the compiler flags in `debian/rules` accordingly.
Be reminded that this source assumes that the the `rules` and especially the modules are located in `/usr/local/src/nginx/nginx-1-16.0/`, 
thus you might have to change the compiler flags according to your file path.

If you want to confugure nginx with ipscrub, you'll require [libbsd](https://libbsd.freedesktop.org/wiki/). Run `apt-get install libbsd-dev` to install it. 

The releases already include debian packages while binaries ending with `full` include all modules (requires libbsd) and the other binary including only the `ngx_headers_more` module.
