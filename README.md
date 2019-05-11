# Documentation
Documentation is available on [nginx](http://nginx.org)

# Project Details
This project is about building Debian packages of the latest nginx versions with late OpenSSL versions. There are various releases differing from each other by the modules added to the package.

To add additional modules, put the modules into the directory `src/modules`, change the compiler flags in `debian/rules` and update possible dependencies under `debian/control` accordingly.

If you want to confugure nginx with ipscrub, you'll require [libbsd](https://libbsd.freedesktop.org/wiki/). Run `apt-get install libbsd-dev` to install it. But the dependencies of the single packages are already set properly, so this shouldn't be a problem.

The releases already include debian packages (.deb file); for more information on the specific packages, see the releases section. The dependencies are set properly while all releases depend on Openssl (≥ 1.1.1b).

# ZStandard Compression
To use the zstd compression module, compile the zstd library first. To do so, the [zstd-nginx-module](https://github.com/mkasimd/zstd-nginx-module) has the [zstd](https://github.com/facebook/zstd) submodule included. Just run the following commands on your CLI to compile and install the zstd library:

```sh
$ cd modules/zstd-nginx-module/zstd
$ make install
```

# Pagespeed
To use the PageSpeed module, you'll require to download the PSOL library and extract it. Details on how to do so is under the config file, though the steps will be like this:

```sh
This is a development branch of ngx_pagespeed, which means there is no
precompiled PSOL library available to link against.  Either build from a
release tag, like latest-beta, or build PSOL from source:
https://github.com/apache/incubator-pagespeed-ngx/wiki/Building-PSOL-From-Source"

You need to separately download the pagespeed library:

$ cd modules/incubator-pagespeed-ngx
$ wget https://www.modpagespeed.com/release_archive/1.14.36.1-incubator-RC0/x64/incubating_psol-1.14.36.1-x64.tar.gz
$ tar -xzvf incubating_psol-1.14.36.1-x64.tar.gz
```

The latest PSOL releases can be found in the [Modpagespeed Release Archive](https://www.modpagespeed.com/release_archive/).

NOTE: [nginx-nonewlines](https://github.com/vedang/nginx-nonewlines) is not added as a module to compile against under `debian/rules` as the PageSpeed module deals with such optimization measures with the right filters enabled already.
