# Documentation
Documentation is available on the [nginx website](http://nginx.org).

# Project Details
This project is about building Debian packages of the latest nginx versions with late OpenSSL versions. There are various releases differing from each other by the modules added to the package.

To add additional modules, put the modules into the directory `src/modules`, change the compiler flags in `debian/rules` and update possible dependencies under `debian/control` accordingly.

If you want to configure nginx with ipscrub, you'll require [libbsd](https://libbsd.freedesktop.org/wiki/). Run `apt-get install libbsd-dev` to install it. But the dependencies of the single packages are already set properly, so this shouldn't be a problem.

The releases already include debian packages (.deb file); for more information on the specific packages, see the releases section. The dependencies are set properly while all releases depend on Openssl (≥ 1.1.1c).

# Versioning
In this project, the Application Versioning (AVer) and the Package Versioning (PVer) are differing from each other. It might sound a little confusing to differ there, but it'll help the user to understand what he is about to install and what he has installed.

## Application Versioning
This is the application version numbering system for KSM-ngx:

 * `<nginx version><openssl version's last letter>-<lite|noPS|full>`

This version numbering will only be displayed when running `nginx -v` or `nginx -V`. By doing so, it is intended that the user can see which build and package of nginx he is using on his system.

## Package & Release Versioning
The package version numbering system varies a little:

 * `<nginx version>.<KSM-ngx release no.>`
  
 This is simply the nginx version followed by a number for the KSM-ngx release built on top of the given nginx version. The reason why this is different is that each application version doesn't really need an own release, but is built on top of the same release anyways and only differ in the modules that the package is compiled with.

# ZStandard Compression
To use the zstd compression module, compile the zstd library first. To do so, the [zstd-nginx-module](https://github.com/mkasimd/zstd-nginx-module) has the [zstd](https://github.com/facebook/zstd) submodule included. Just run the following commands on your CLI to compile and install the zstd library:

```sh
$ cd src/modules/zstd-nginx-module/zstd
$ make install
```

# Pagespeed
To use the PageSpeed module, you'll require to download the PSOL library and extract it. 

## Automated Configuration
You can configure the PageSpeed module automaticalls by using the script provided by pagespeed/ngx_pagespeed [here](https://ngxpagespeed.com/install).

## Manual Configuration
Details on how to do so is under the config file, though the steps will be like this:

```sh
This is a development branch of ngx_pagespeed, which means there is no
precompiled PSOL library available to link against.  Either build from a
release tag, like latest-beta, or build PSOL from source:
https://github.com/apache/incubator-pagespeed-ngx/wiki/Building-PSOL-From-Source"

You need to separately download the pagespeed library:

$ cd src/modules/incubator-pagespeed-ngx
$ wget https://www.modpagespeed.com/release_archive/1.14.36.1-incubator-RC0/x64/incubating_psol-1.14.36.1-x64.tar.gz
$ tar -xzvf incubating_psol-1.14.36.1-x64.tar.gz
```

The latest PSOL releases can be found in the [Modpagespeed Release Archive](https://www.modpagespeed.com/release_archive/).

NOTE: [nginx-nonewlines](https://github.com/vedang/nginx-nonewlines) is not added as a module to compile against under `debian/rules` as the PageSpeed module deals with such optimization measures with the right filters enabled already.

# Modules
KSM-ngx comes with three types of releases, namely `lite`, `noPS` and `full`. They all have the same nginx base, but differ from each other with the modules that are provided. See the notes for each release to see which modules each provided package come with. Additionally, you can check out [mkasimd/nginx-modules](https://github.com/mkasimd/nginx-modules) to see some additional useful modules which might not be included in the releases.
