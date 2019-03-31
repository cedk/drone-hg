# drone-hg

[![Build Status](http://cloud.drone.io/api/badges/drone-plugins/drone-hg/status.svg)](http://cloud.drone.io/drone-plugins/drone-hg)
[![Gitter chat](https://badges.gitter.im/drone/drone.png)](https://gitter.im/drone/drone)
[![Join the discussion at https://discourse.drone.io](https://img.shields.io/badge/discourse-forum-orange.svg)](https://discourse.drone.io)
[![Drone questions at https://stackoverflow.com](https://img.shields.io/badge/drone-stackoverflow-orange.svg)](https://stackoverflow.com/questions/tagged/drone.io)
[![](https://images.microbadger.com/badges/image/plugins/hg.svg)](https://microbadger.com/images/plugins/hg "Get your own image badge on microbadger.com")
[![Go Doc](https://godoc.org/github.com/drone-plugins/drone-hg?status.svg)](http://godoc.org/github.com/drone-plugins/drone-hg)
[![Go Report](https://goreportcard.com/badge/github.com/drone-plugins/drone-hg)](https://goreportcard.com/report/github.com/drone-plugins/drone-hg)

Drone plugin to clone `mercurial` repositories. For the usage information and a listing of the available options please take a look at [the docs](http://plugins.drone.io/drone-plugins/drone-hg/).

## Build

Build the binary with the following command:

```console
export GOOS=linux
export GOARCH=amd64
export CGO_ENABLED=0
export GO111MODULE=on

go build -v -a -tags netgo -o release/linux/amd64/drone-hg
```

## Docker

Build the Docker image with the following command:

```console
docker build \
  --label org.label-schema.build-date=$(date -u +"%Y-%m-%dT%H:%M:%SZ") \
  --label org.label-schema.vcs-ref=$(git rev-parse --short HEAD) \
  --file docker/Dockerfile.linux.amd64 --tag plugins/hg .
```

## Usage

Clone a commit:

```console
docker run --rm \
  -e DRONE_REMOTE_URL=https://bitbucket.org/cedk/drone-hg-test \
  -e DRONE_WORKSPACE=/go/src/bitbucket.org/cedk/drone-hg-test \
  -e DRONE_BUILD_EVENT=push \
  -e DRONE_COMMIT_SHA=d8dbe4d94f15fe89232e0402c6e8a0ddf21af3ab \
  -e DRONE_COMMIT_REF=refs/heads/master \
  plugins/hg
```

Clone a pull request:

```console
docker run --rm \
  -e DRONE_REMOTE_URL=https://bitbucket.org/cedk/drone-hg-test \
  -e DRONE_WORKSPACE=/go/src/bitbucket.org/cedk/drone-hg-test \
  -e DRONE_BUILD_EVENT=pull_request \
  -e DRONE_COMMIT_SHA=3b4642018d177bf5fecc5907e7f341a2b5c12b8a \
  -e DRONE_COMMIT_REF=refs/pull/74/head \
  plugins/hg
```

Clone a tag:

```console
docker run --rm \
  -e DRONE_REMOTE_URL=https://bitbucket.org/cedk/drone-hg-test \
  -e DRONE_WORKSPACE=/go/src/bitbucket.org/cedk/drone-hg-test \
  -e DRONE_BUILD_EVENT=tag \
  -e DRONE_COMMIT_SHA=3b4642018d177bf5fecc5907e7f341a2b5c12b8a \
  -e DRONE_COMMIT_REF=refs/tags/74/head \
  plugins/hg
```
