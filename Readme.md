# OONI Probe CLI

The next generation OONI Probe Command Line Interface.

## Development setup

Be sure you have golang >= 1.8.

This project uses [`dep`](https://golang.github.io/dep/) with the `vendor/` dir
in `.gitignore`.

Once you have `dep` installed, run:

```
dep ensure
```

Next, you'll need a recent version of [Measurement Kit](http://github.com/measurement-kit).

Building a ooni binary for windows and macOS is currently only supported on a
macOS system.

For building a linux ooni binary, you will need a linux system and follow the
intruction in the linux section.

### macOS

On macOS you can build a windows and macOS ooni binary.

This can be done by running:

```
make download-mk-libs
```

This will download the prebuilt measurement-kit binaries.

Then you can build a macOS build by running:

```
make build
```

And a windows build by running:

```
make build-windows
```

### linux

On linux you will have to make your own build of measurement-kit and the
required dependencies.

The following instructions have been tested on debian stretch, but should work
on any other modern debian equivalent with minor tweaks.

Install the required depedencies:

```
sudo apt-get install git build-essential cmake autoconf libtool golang libc++-dev
```

Note: be sure you have golang at >= 1.8 (debian stretch means using backports).

```
git clone https://github.com/measurement-kit/script-build-unix.git
cd script-build-unix
```

Then build measurement-kit as follows:

```
./build-linux geoip-api-c
./build-linux libressl
./build-linux libevent
./build-linux measurement-kit
```

You should now have a set of compiled libraries inside of `MK_DIST`. Take this and copy it into `vendor/github.com/measurement-kit/go-measurement-kit/libs/linux`.

It should now be possible to build ooni by running:

```
make build
```

To run internal tests do:

```
make test-internal
```
