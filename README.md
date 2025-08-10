# multi-room-audio
Using Mopidy and Snapcast to synchronise playback between multiple Linux devices on a home network

Mopidy is an audio playback service which allows you to play files or network streams, and has a variety of useful plugins. The Snapcast service allows for multiple audio playback devices to be synchronised with each other, and works well over ethernet or wifi in a home network. The audio output from a mopidy server can be sent to a snapserver process, and multiple devices running snapclient can be configured to play audio.

## Components

### [Mopidy](https://docs.mopidy.com/stable/installation/).

Once Mopidy is installed, it can be configured to use a variety of audio sources such as local files, online streams and with [various extensions](https://mopidy.com/ext/) such as [Tidal](https://mopidy.com/ext/tidal/), [Bandcamp](https://mopidy.com/ext/bandcamp/) or [Soma FM](https://mopidy.com/ext/somafm/).

An example line from /etc/mopidy/mopidy.conf from the audio section is shown below which will send its output to the named pipe used by a Snapcast server running locally as snapserver.

output = audioresample ! audio/x-raw,rate=48000,channels=2,format=S16LE ! audioconvert ! wavenc ! filesink location=/tmp/snapfifo

### Snapcast

Snapcast consists of a server daemon, snapserver, configured to accept an audio stream via a named pipe in this case, and multiple devices running snapclient which connect to the server 

https://github.com/badaix/snapcast

### Hardware

