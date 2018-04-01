# Docker Machine VMware Workstation Driver

[![Join the chat at https://gitter.im/pecigonzalo/docker-machine-vmwareworkstation](https://badges.gitter.im/pecigonzalo/docker-machine-vmwareworkstation.svg)](https://gitter.im/pecigonzalo/docker-machine-vmwareworkstation?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Windows Build Status](https://ci.appveyor.com/api/projects/status/k8j7ej2a7t58p2r0/branch/master?svg=true)](https://ci.appveyor.com/project/pecigonzalo/docker-machine-vmwareworkstation)

This plugin for [Docker Machine](https://docs.docker.com/machine/) creates
Docker hosts locally on a [VMware
Workstation](https://www.vmware.com/products/workstation).

This is a placeholder and collaboration point to add a VMware workstation
driver for Docker Machine. This driver reuses part of the code from the [fusion
driver](https://github.com/docker/machine/tree/master/drivers/vmwarefusion)
bundled with Docker Machine (as both have the same executable) and includes
additional code from [Packer](https://packer.io) VMware driver to detect the
location of the files on Windows systems.

This is still a work-in-progress (WIP). I'm working to add the functionality
listed on the TODO list. Suggestions and contributions are welcome.

## TODO

* ~~drivers/vmwareworkstation/workstation.go: Rework file for vmware workstation~~
* ~~add windows support~~
* ~~add cmd/machine-driver-vmwareworkstation.go~~
* Add Linux/OSX support
* ~~Add dhcplease file discovery on windows~~
* Add tests cases
* ~~Create makefile~~
* Add docs/drivers/vm-workstation.md

## Requirements

* Windows 7+ (for now)
* [Docker Machine](https://docs.docker.com/machine/) 0.5.0+
* [VMware Workstation](https://www.vmware.com/products/workstation) Workstation Free/Pro 10 +

## Installation

The latest version of `docker-machine-driver-vmwareworkstation` binary is
available on the
["Releases"](https://github.com/pecigonzalo/docker-machine-vmwareworkstation/releases)
page.

Place the executable in the directory containing `docker-machine.exe`, or else
add it to your $PATH.

## Installing with Docker Toolbox

1. Install Docker Toolbox without VirtualBox

    `DockerToolbox.exe /COMPONENTS="Docker,DockerMachine"`

2. Use this repository start.sh file Replace of `C:\Program Files\Docker Toolbox\start.sh`.

    Credit for the above script to [@gtirloni](https://github.com/gtirloni)

## Usage

Official documentation for Docker Machine is available
[here](https://docs.docker.com/machine/).

To create a VMware Workstation based Docker machine, just run this
command:

```bash
docker-machine create --driver=vmwareworkstation dev
```

## Options

* `--vmwareworkstation-boot2docker-url`: The URL of the [Boot2Docker](https://github.com/boot2docker/boot2docker) image.
* `--vmwareworkstation-disk-size`: Size of disk for the host VM (in MB).
* `--vmwareworkstation-memory-size`: Size of memory for the host VM (in MB).
* `--vmwareworkstation-cpu-count`: Number of CPUs to use to create the VM (-1 to use the number of CPUs available).
* `--vmwareworkstation-ssh-user`: SSH user
* `--vmwareworkstation-ssh-password`: SSH password

The `--vmwareworkstation-boot2docker-url` flag takes a few different forms. By
default, if no value is specified for this flag, Machine checks locally for a
Boot2Docker ISO. If one is found, that will be used as the ISO for the new
machine. If one is not found, the latest ISO release available on
[boot2docker/boot2docker](https://github.com/boot2docker/boot2docker) will be
downloaded and stored locally for future use. Note that this means you must run
`docker-machine upgrade` deliberately on a machine if you wish to update the
"cached" Boot2Docker ISO.

This is the default behavior (when `--vmwareworkstation-boot2docker-url=""`),
but the option also supports specifying ISOs by the `http://` and `file://`
protocols.

Environment variables and default values:

| CLI option                            | Environment variable          | Default                  |
| ------------------------------------- | ----------------------------- | ------------------------ |
| `--vmwareworkstation-boot2docker-url` | `WORKSTATION_BOOT2DOCKER_URL` | *Latest boot2docker url* |
| `--vmwareworkstation-cpu-count`       | `WORKSTATION_CPU_COUNT`       | `1`                      |
| `--vmwareworkstation-disk-size`       | `WORKSTATION_DISK_SIZE`       | `20000`                  |
| `--vmwareworkstation-memory-size`     | `WORKSTATION_MEMORY_SIZE`     | `1024`                   |
| `--vmwareworkstation-ssh-user`        | `WORKSTATION_SSH_USER`        | `docker`                 |
| `--vmwareworkstation-ssh-password`    | `WORKSTATION_SSH_PASSWORD`    | `tcuser`                 |

## Development

### Build from Source

If you wish to work on VMware Workstation Driver for Docker machine, you'll
first need:

* [Go](http://www.golang.org) installed (version 1.6+ is required).
  * Make sure Go is properly installed, including setting up a [GOPATH](http://golang.org/doc/code.html#GOPATH).

* [MSYS](https://msys2.github.io/)
  * **Make** We well need to use pacman to install make

* Currently, the build only works on Windows (WIP to get it to work on
  other platforms)

To build the plugin executable binary, run these commands:

```bash
go get -d github.com/pecigonzalo/docker-machine-vmwareworkstation
cd $GOPATH/github.com/pecigonzalo/docker-machine-vmwareworkstation
make
```

The build creates the binary as `bin/docker-machine-driver-vmwareworkstation`. If you want, copy it to `${GOPATH}/bin/`.

## Authors

* Gonzalo Peci ([@pecigonzalo](https://github.com/pecigonzalo))

## Credits

* Partial copy of the README from https://github.com/Parallels/docker-machine-parallels
* [Packer](https://packer.io) VMware Workstation driver functions
* [gtirloni](https://github.com/gtirloni) Instructions for Docker Toolbox
