---
layout: post
title: How I installed GDAL on a Mac (El Capitan)
published: True
---

I work with a lot of geospatial data, and I depend on a system installation of GDAL.  GDAL lets me open geo-referenced TIF images, and it's a dependency for a lot of python packages like Shapely and GeoPandas.  If all I needed to do was use GDAL in python, I could try to install it through Anadona (`conda install -c https://conda.anaconda.org/ioos geopandas=0.2.1` note: this doesn't like python 3.6, so you might need to create a virtual environment with 3.5), but I also like to use some of GDAL's command like tools like `gdalinfo` and `gdal_pansharpen.py`.  So I had to suffer through a system-wide install for mac, which is a challenge.

## The legends say this can be done easily...
I have heard legends that say this is as easy as installing from a keg in homebrew, but I was unable to confirm these legends. Maybe you want to give it a try anyway...
```
brew tap osgeo/osgeo4mac
brew install gdal2 
```

If that doesnt work for you, then read on.

## What worked for me
I tried to build GDAL from source, but I had to deal with a lot of version conflicts to make it work.  At the system level on a mac, some of the packages are the wrong version and some others are just not in the right place where the installer will look for them.  I handled this using a few different tricks:
* Telling GDAL to use interal packages whenever possible (jpeg, libtiff, etc)
* Forcing homebrew to link some packanges
* Pointing the GDAL installer to some of the binaries it would need

Before trying this out, I should warn you that this stuff is dangerous, and there's no easy way to uninstall GDAL after you do this.  Forcing homebrew to link to packages that come with OSX could cause problems.  I have not had any problems since I did this, but that's no guarantee that you won't.

Ok, now that I've warned you, here's what I did:

```
brew install postgresql
brew link curl --force
brew link libxml2 --force

# Install and link libiconv... the most dangerous game
brew install homebrew/dupes/libiconv
brew link --force libiconv

./configure --with-python --with-jpeg=internal --with-png=internal --with-geotiff=internal --with-libtiff=internal --with-curl=/usr/local/bin/curl  CPPFLAGS="-I/usr/local/opt/openssl/include" LDFLAGS="-L/usr/local/opt/openssl/lib"
make -j4
sudo make install
```

Now it should be installed, so sest it out by running `gdalinfo`
```
$ gdalinfo --version
GDAL 2.2.0dev, released 2016/99/99
```

If this works, then great, you're done.  If you get a linker error, you might need to install or link a package.


