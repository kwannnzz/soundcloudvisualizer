# Soundcloud Visualizer

This is an experiment in using the web audio API together with canvas to make some interesting and cool-looking visualizations.

Since this is my first foray into the world of both canvas and web audio, I have slowly iterated over a number of ideas and trials which are all in the /tests folder.

The visual style was inspired by the artwork of the album ["The Resistance"] (http://en.wikipedia.org/wiki/File:Theresistance.jpg) by Muse.

# Instructions

Go to https://soundcloud.com and find some music. From the individual song page, copy the url and paste it into the input of the visualizer, then hit enter or press the play button.

You'll notice that part of the the track URL is added to the visualizer's URL. This makes it possible to easily save or share the state. So, if you find a good track that looks cool with
 the visualization that you want to share, just give the new URL to someone and when they load it up, it'll automatically start streaming and visualizing that track.

# Issues

Since the web audio API is pretty new, browser support is patchy:

- *Chrome* Latest versions works well, that's what I've been building in.
- *Firefox* This *should* work, since it has supported web audio since version 25, but in my tests the audio fails to play. Any suggestions?
- *Safari* I haven't tested it since I'm stuck with the dead Windows version, but I guess it should work since it's WebKit.
- *IE* Nope.
- *Opera* Not tested but maybe now that they switched to WebKit.

# Improvements

I can think of a few improvements that I might implement, or someone else might want to:

- Support for playlists. So you can paste the playlist URL and it just keeps going through to the end of the playlist.
- More types of visualization. I've written the code in a pretty modular way so it's simple to write a visualization that can plug into the app (see below)
- Better browser support. I'm sure there can be more done on this to get it working at least in Firefox and mobile WebKit browsers, with perhaps fallbacks for IE.

# Writing visualizations

If you want to fork this and write your own visualizations, they way I've set it up is pretty simple:
The audio data from Soundcloud is processed by the SoundCloudAudioSource object, which exposes two properties, `volume` and `streamData`, which are continuously updated in real-time.

`streamData` is an array of 128 integers from 0-255, representing the volume of the signal at each frequency.
`volume` is a single integer representing the overall volume, useful for things like pulsing effects that reflect the beat of the audio track.

Your visualization object just needs to consume this object and then it will be able to do whatever it wants to with the data provided. The visualization object should make
it's own canvas elements and append them to the `#visualizer` div.
