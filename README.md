# multi-room-audio
Using Mopidy and Snapcast to synchronise playback between multiple Linux devices on a home network

Mopidy is an audio playback service which allows you to play files or network streams, and has a variety of useful plugins. The audio output from a mopidy server can be sent to a snapserver process, and multiple devices running snapclient can be configured to play back synchronised audio.

Components

Mopidy installation documentation is available from https://docs.mopidy.com/stable/installation/

Once Mopidy is installed, it can be configured to use a variety of audio sources such as local files, online streams and with [various extensions](https://mopidy.com/ext/) such as [Tidal](https://mopidy.com/ext/tidal/), [Bandcamp](https://mopidy.com/ext/bandcamp/) or [Soma FM](https://mopidy.com/ext/somafm/).
