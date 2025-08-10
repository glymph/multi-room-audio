# multi-room-audio
Using Mopidy and Snapcast to synchronise playback between multiple Linux devices on a home network

Mopidy is an audio playback service which allows you to play files or network streams, and has a variety of useful plugins. The Snapcast service allows for multiple audio playback devices to be synchronised with each other, and works well over ethernet or wifi in a home network. The audio output from a mopidy server can be sent to a snapserver process, and multiple devices running snapclient can be configured to play audio.

## Components

### [Mopidy](https://docs.mopidy.com/stable/installation/)

Once Mopidy is installed, it can be configured to use a variety of audio sources such as local files, online streams and with [various extensions](https://mopidy.com/ext/) such as [Tidal](https://mopidy.com/ext/tidal/), [Bandcamp](https://mopidy.com/ext/bandcamp/) or [Soma FM](https://mopidy.com/ext/somafm/). An [MPD extension](https://mopidy.com/ext/mpd/) is also available to allow compatible clients to control playback on the Mopidy server using the Music Player Daemon protocol.

An example line from /etc/mopidy/mopidy.conf from the audio section is shown below which will send its output to the named pipe used by a Snapcast server running locally as snapserver.
```
output = audioresample ! audio/x-raw,rate=48000,channels=2,format=S16LE ! audioconvert ! wavenc ! filesink location=/tmp/snapfifo
```
### [Snapcast](https://github.com/badaix/snapcast)

Snapcast consists of a server daemon, snapserver, configured to accept an audio stream via a named pipe in this case, and multiple devices running snapclient which connect to the server. The client daemon can be run locally on the server to play audio through its own hardware, and other devices will connect via the local network to the server. Either wifi or ethernet cable can be used for the Snapcast clients, and the network and processing requirements are minimal. 

An example snapserver configuration line in the stream section of /etc/snapserver.conf is shown below.
```
source = pipe:///tmp/snapfifo?name=default
```
### Hardware

Snapclient can be run on any device capable of installing the client application and caching and playing audio across the local network, such as a Raspberry Pi, ESP32 or mobile handset. There are also various hardware solutions for the Raspberry Pi such as the [HifiBerry](https://www.hifiberry.com/shop/#boards) or [Pirate Audio](https://github.com/pimoroni/pirate-audio) series of HATs. 

One particular advantage of the HifiBerry series of boards is that the company which manufactures the boards also provides a preconfigured linux distribution which has a web interface, and has various audio clients preconfigured. It is possible to cast from an Apple device to it temporarily, for example, even if the HifiBerry device is part of a Snapcast configuration. After casting has finished, the HifiBerry device will return to being part of the Snapcast configuration. HifiBerry devices are available either with built-in amplifiers or with various different line-out options such as 3.5mm sockets, RCA or optical connectors. Cases which accomodate the Raspberry Pi and HifiBerry board with its connectors are also available.

Although the Raspberry Pi has no volume control, there are several options for controling the output of the clients in this kind of configuration. The volume can be controlled for all playback devices via the server on its browser interface, via an extension such as MPD, or indiviually on the clients. Using HifiBerry clients, the volume can be adjusted individually from each one's browser inferface, or via an attached keyboard with volume up/down buttons. Alternatively, these keyboard inputs can be sent from an Arduino capable of acting as a USB host device, as described in [in a separate project page](https://github.com/glymph/ArduinoVolumeControl).



