# About
Modified source code from: https://github.com/kevineye/docker-shairport-sync

## Intro
[shairport-sync](https://github.com/mikebrady/shairport-sync) is an Apple
AirPlay receiver. It can receive audio directly from iOS devices, iTunes, etc.
Multiple instances of shairport-sync will stay in sync with each other and other
AirPlay devices when used with a compatible multi-room player, such as iTunes or
[forked-daapd](https://github.com/jasonmc/forked-daapd).

## Multi-arch Image
The below commands reference a
[Docker Manifest List](https://docs.docker.com/engine/reference/commandline/manifest/)
at `tigerj/shairport-sync`. Simply running commands using this image will pull
the matching image architecture (e.g. `amd64`, `arm32v7`) based on the hosts
architecture. Hence, if you are on a **Raspberry Pi** the below commands will
work the same as if you were on a traditional `amd64` desktop/laptop computer.

## Run
To simply run a container from the image in `daemon` mode:
```
docker run -d \
       --net host \
       --device /dev/snd \
       -e AIRPLAY_NAME=shairport-sync \
       tigerj/shairport-sync
```

## Create
To create a container from the image (for later use):
```
docker create \
       --restart=always \
       --name=shairport-sync \
       --net=host \--device /dev/snd \
       -e AIRPLAY_NAME="shairport-sync" \
       tigerj/shairport-sync
```
Then run this container by name using `docker start`:
```
docker start shairport-sync
```

### Parameters
* `--net host` must be run in host mode
* `--device /dev/snd` share host alsa system with container. Does not require
`--privileged` as `-v /dev/snd:/dev/snd` would
* `-e AIRPLAY_NAME=Docker` set the AirPlay device name. If unset it defaults to
"Docker"
* extra arguments will be passed to shairplay-sync (try `-- help`)

## ToDo
* Pin os version in base image of dockerfile
* Add default volume for shairport-sync
