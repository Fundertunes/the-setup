The Setup
=========

This repo will help developers and administrators bootstrap a Fundertunes
environment. Services are managed with Docker and run through Vagrant.

At it's core, Fundertunes utilizes [MPD](http://www.musicpd.org/) for music
playback and [Icecast](http://www.icecast.org/) for streaming over networks. Each of these services are
siloed into their own Docker containers.

## Prerequisites
* Vagrant (>= 1.6)
* VirtualBox or other VM software (only necessary for platforms that don't
support Linux containers - so basically anything other than Linux)
* mpc (Optional, but useful command line utility to interact with MPD -
  available via your favorite package manager)

## Getting Started
To bootstrap a basic environment, simply run the following:
```shell
vagrant up icecast mpd --provider=docker
```

The order in which the images are specified is important as the MPD
container expects the Icecast container to already be running when it starts.

## Playing Some Tunes
The `/music` directory in this repo is synced with the Vagrant environment and
then mounted as a volume within the MPD container. This mechanism is liable to
change in the future, but it serves its purpose for now.

To play music, simply add some songs to the `/music` directory and run the
following (assuming you've installed mpc):
```shell
mpc update
mpc ls | mpc add
mpc playlist
mpc play
```

The `mpc playlist` command should output the names of any files you've added to the
`/music` directory.

Assuming everything went properly, you should now be able to browse to
localhost:8000 and see the Icecast status page and be able to play your stream.
Simply select the protocol you want to use, open the downloaded file, and enjoy!

## License
The Setup is distributed under the MIT License. See LICENSE for details.
