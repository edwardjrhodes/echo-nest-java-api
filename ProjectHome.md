<img src='http://developer.echonest.com/media/images/DN_Logo.gif' />
<p>
This is a Java API and assorted tools and helpers for the Echo Nest API (at <a href='http://developer.echonest.com'>developer.echonest.com</a>).<br>
<br>
Note - for a version of the API that works with Version 4 of the Java API see <a href='http://code.google.com/p/jen-api/'>jEN-api</a>

<b>Table of Contents</b>
<br>
<br>
<br>
<h1>The Echo Nest API Overview</h1>

The Echo Nest API is divided into two sets of methods: Artist methods and track methods.<br>
<br>
<h2>Artist Methods</h2>

Some of the Echo Nest artist capabilities:<br>
<br>
<ul><li>get a list of the hottest artists<br>
</li><li>search for artists<br>
</li><li>get news about an artist<br>
</li><li>get reviews about an artist<br>
</li><li>get blogs about an artist<br>
</li><li>get urls for an artist<br>
</li><li>get video for an artist<br>
</li><li>find audio for an artist<br>
</li><li>find familiarity and hotttness of an artist</li></ul>

<h2>Track methods</h2>

Some of the Echo Nest track capabilities:<br>
<br>
<ul><li>Upload a track for analysis<br>
</li><li>Get metadata for a track<br>
</li><li>get the overall key of a track<br>
</li><li>Get the overall loudness of a track<br>
</li><li>Get the overall time signature of a track<br>
</li><li>Get the overall tempo of a track<br>
</li><li>Get the duration of a track<br>
</li><li>Get the mode (major/minor) of a track<br>
</li><li>Get the fade-in and fade-out times for a track<br>
</li><li>Get a detailed analysis of the beat structure of a song including sections, bars, beats and tatums<br>
</li><li>Get timbral, pitch and loudness information for every sound event in the track</li></ul>

<h1>Getting Started</h1>
<ul><li><a href='http://code.google.com/p/echo-nest-java-api/downloads/list'>Download the latest release</a>
</li><li>Unzip the archive<br>
</li><li>Add the EchoNestAPI.jar file to your CLASSPATH<br>
</li><li>Browse some of the <a href='http://code.google.com/p/echo-nest-java-api/source/browse/trunk/src/examples/'>code samples</a>
</li><li>Get an API key from <a href='http://developer.echonest.com'>developer.echonest.com</a>
</li><li>Browse the <a href='http://echo-nest-java-api.googlecode.com/svn/tags/v1.3a/javadoc/index.html'>Javadocs</a> included with the distribution</li></ul>

<h1>Code Examples</h1>
<h2>Artist Similarity Example</h2>
Here's an example of code to print out all artists that are similar to 'Weezer'<br>
<br>
<pre><code>   ArtistAPI artistAPI = new ArtistAPI(MY_ECHO_NEST_API_KEY);<br>
<br>
   List&lt;Artist&gt; artists = artistAPI.searchArtist("weezer", false);<br>
<br>
   for (Artist artist : artists) {<br>
        List&lt;Scored&lt;Artist&gt;&gt; similars = artistAPI.getSimilarArtists(artist, 0, 10);<br>
        for (Scored&lt;Artist&gt; simArtist : similars) {<br>
            System.out.println("   " + simArtist.getItem().getName());<br>
        }<br>
    }<br>
  <br>
<br>
</code></pre>

<h2>Artist Audio example</h2>
Use the Echo Nest Artist API to find audio for an artist<br>
<br>
<pre><code><br>
   ArtistAPI artistAPI = new ArtistAPI(MY_ECHO_NEST_API_KEY);<br>
<br>
   List&lt;Artist&gt; artists = artistAPI.searchArtist("The Decemberists", false);<br>
   for (Artist artist : artists) {<br>
       DocumentList&lt;Audio&gt; audioList = artistAPI.getAudio(artist, 0, 15);<br>
       for (Audio audio : audioList.getDocuments()) {<br>
          System.out.println(audio.toString());<br>
       }<br>
   }<br>
<br>
<br>
</code></pre>


<h2>Track BPM example</h2>
Here's some sample code to determine the average BPM for a track:<br>
<br>
<pre><code>    TrackAPI trackAPI = new TrackAPI(MY_ECHO_NEST_API_KEY);<br>
<br>
    String id = trackAPI.uploadTrack(new File("/path/to/music/track.mp3"), false);<br>
    AnalysisStatus status = trackAPI.waitForAnalysis(id, 60000);<br>
    if (status == AnalysisStatus.COMPLETE) {<br>
       System.out.println("Tempo in BPM: " + trackAPI.getTempo(id));<br>
    }                 <br>
</code></pre>


<h1>Running the examples</h1>


<h2>FindSimilarArtists</h2>
<pre>
$ *java -DECHO_NEST_API_KEY=$MY_ECHO_NEST_KEY -cp EchoNestAPI.jar  examples.FindSimilarArtists 'weezer'*<br>
<br>
---- Similar artists for Weezer ----<br>
Nerf Herder<br>
The Smashing Pumpkins<br>
Third Eye Blind<br>
Ozma<br>
Fountains of Wayne<br>
Nada Surf<br>
Ben Folds Five<br>
The Flaming Lips<br>
Jimmy Eat World<br>
Death Cab for Cutie<br>
Veruca Salt<br>
Sunny Day Real Estate<br>
They Might Be Giants<br>
Alkaline Trio<br>
Rivers Cuomo<br>
</pre>

<h3>FindArtistAudio</h3>
<pre>
$ *java -DECHO_NEST_API_KEY=$MY_ECHO_NEST_KEY -cp EchoNestAPI.jar  examples.FindArtistAudio 'The Decemberists'*<br>
<br>
---- Audio for The Decemberists ----<br>
artist: The Decemberists<br>
artist_id: music://id.echonest.com/~/AR/ARHWR8B1187FB557D3<br>
length: 195.0<br>
link: http://theyellowstereo.com/2009/03/the-daily-graboid-69/<br>
release: The Hazards Of Love<br>
title: The Rake's Song<br>
url: http://www.theyellowstereo.com/Daily%20Graboid/week2/The%20Decemberists%20-%20The%20Rake%27s%20Song.mp3<br>
<br>
artist: The Decemberists<br>
artist_id: music://id.echonest.com/~/AR/ARHWR8B1187FB557D3<br>
length: 299.0<br>
link: http://passionweiss.com<br>
release: Always The Bridesmaid: A Singles Series<br>
title: Valerie Plame<br>
url: http://passionweiss.com/wp-content/uploads/2008/12/01-valerie-plame.mp3<br>
<br>
_(entries omitted)_<br>
<br>
</pre>

<h3>The debug shell</h3>
The API also includes an interactive shell that lets you easily interact with the Echo Nest API. Some examples:<br>
<br>
<pre>
*java -DECHO_NEST_API_KEY=$MY_ECHO_NEST_KEY -cp EchoNestAPI.jar  com.echonest.api.v3.test.EchonestDevShell*<br>
<br>
nest% *search_artist blitzen*<br>
<br>
music://id.echonest.com/~/AR/ARMT1QJ1187FB3D555 Blitzen<br>
music://id.echonest.com/~/AR/ARKHKCO1187FB429D0 Rudolph & Blitzen<br>
music://id.echonest.com/~/AR/ARJ3IUO1187B999C26 Donner & Blitzen<br>
music://id.echonest.com/~/AR/ARXWFZ21187FB43A0B Blitzen Trapper<br>
<br>
<br>
nest% *get_audio blitzen trapper*<br>
<br>
Audio for Blitzen Trapper<br>
Total audio 107<br>
id: 9b634d44a89839038a8fc30b0dcc03a9 type: audio<br>
title: Texaco<br>
artist: Blitzen Trapper<br>
artist_id: music://id.echonest.com/~/AR/ARXWFZ21187FB43A0B<br>
release: Dead Bees Label Sampler #2<br>
url: http://media.deadbees.com/sampler_02/Dead%20Bees%20Sampler%202%20-%2003%20-%20Blitzen%20Trapper%20-%20Texaco.mp3<br>
<br>
_(etc)_<br>
<br>
<br>
nest% *trackUpload /Users/plamere/Music/Amazon MP3/The Decemberists/Hazards Of Love/13 - Annan Water.mp3*<br>
<br>
ID: music://id.echonest.com/~/TR/TRINNMV1208142F431<br>
<br>
<br>
nest% *trackMetadata music://id.echonest.com/~/TR/TRINNMV1208142F431*<br>
<br>
Artist    : The Decemberists<br>
Release   : Hazards Of Love<br>
Title     : Annan Water<br>
Genre     : Pop<br>
Duration  : 311.4291<br>
Samplerate: 44100<br>
Bitrate   : 263<br>
<br>
nest% *trackTempo music://id.echonest.com/~/TR/TRINNMV1208142F431*<br>
<br>
101.963 (0.444)<br>
<br>
<br>
nest% *help*<br>
<br>
_(shows you the 60 or so available commands)_<br>
<br>
</pre>


<br>
<br>
<a href='http://the.echonest.com'> <img src='http://the.echonest.com/media/images/logos/250x80_lt.gif' /></a>