<!-- - Copyright © 2021 Bedag Informatik AG Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0 Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License. -->

 # squid Docker Image

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) ![docker-publish](https://github.com/bedag/docker-squid/workflows/docker-publish/badge.svg) [![Dockerhub](https://img.shields.io/docker/pulls/bedag/squid?style=plastic)](https://hub.docker.com/r/bedag/squid)

![Bedag](https://www.bedag.ch/wGlobal/wGlobal/layout/images/logo.svg)

This is a docker project for [squid](https://github.com/squid/squid/).

## Usage

Run the container like this:

```
docker run -v /usr/local/squid/etc:${PWD}/config bedag/squid:<tag>
```

## Volumes

Make sure that all volumes are owned by nobody(65534).

Mountpoint                            | Description
------------------------------------- | ----------------------------------
/usr/local/squid/etc        | configuration files for squid
/usr/local/squid/var/logs        | log files for squid
/usr/local/squid/var/run | pid for squid

## Build

Docker builds are created with [bedag/image-build](https://github.com/bedag/image-build).

[musl compiler](https://www.musl-libc.org/how.html) is used to compile squiduardian.

`gcr.io/distroless/cc` are used because we do not need any common linux binaries, [here](https://github.com/GoogleContainerTools/distroless) you can find more information about distroless images. For troubleshooting we recommend to use our `-debug` images. For more information go to [Debug](#Debug) section.

Every Sunday(`0 0 * * SUN`) we automatically update all [supported tags](#Tags) with the current upstream image.

## Debug

In our production image there are no binaries for troubleshooting. Therefore if u like to troubleshoot you should use our debug image like this:

```
docker run -it bedag/squid:latest-debug
docker run -it bedag/squid:5-debug
```

In the debug image busybox is installed. You can find all busybox supported commands like this:

```
busybox --list
```

## Tags

Supported tags are:

- `latest`, `5`, `5.0`, `5.0.4`, `latest-debug`, `5-debug`, `5.0-debug`, `5.0.4-debug`
- `4`, `4.13`,`4-debug`, `4.13-debug`

## Security notice

Security scans are performed via [trivy](https://github.com/aquasecurity/trivy) and reported in [github](./security). Scans are only performed to the `latest` tag, which should include all libs vulnerabilities from all possible tags.

## Contributing

We'd love to have you contribute! Please refer to our [contribution guidelines](CONTRIBUTING.md) for details.

**By making a contribution to this project, you agree to and comply with the [Developer's Certificate of Origin](./DCO).**

## License

[Apache 2.0 License](./LICENSE).
