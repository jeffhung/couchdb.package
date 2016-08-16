# Package: couchdb

Package couchdb in RPM/DEB formats.

PS: DEB is not supported, yet.


## Prerequisites

To build the packages, you need the following prerequisites:

* [Vagrant](https://www.vagrantup.com/)
* [Ansible](https://www.ansible.com/)
* [GNU make](https://www.gnu.org/software/make/)

And these utilities will be downloaded automatically:

* [rpm.make](https://github.com/jeffhung/rpm.make)
* [jeffhung.couchdb](https://galaxy.ansible.com/jeffhung/couchdb/)
* [jeffhung.localrepo](https://galaxy.ansible.com/jeffhung/localrepo/)


## Usage

Run the following command to build RPM package:

```console
make rpm
```

Run the following command to build DEB package:

```console
make deb
```

Run the following command to launch `couchdb`:

```console
make run
```

Type `make help` to see more options.

```console
$ make help
Usage: make [ TARGET ... ]

TARGET:

  help      - show this help message
  rpm       - package as RPM file (in builder)
  deb       - package as DEB file (in builder)
  run       - install and run the package (in runner)
  stop      - stop builder/runner instances
  clean     - delete all generated files
  distclean - delete all generated files and caches

Default TARGET is 'help'.
```


## License

BSD


