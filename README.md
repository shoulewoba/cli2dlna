cli2dlna
========

cli2dlna: CLI to DLNA
---------------------

Command line tool to play media on remote renderers.  
This is just a Proof-Of-Concept code and it has some limitations.  
Right now:
- it can work with only one renderer.
- limited number of functions (stop/start/pause/play)
- it does not share your media via http.
  This should be done by other stuff, like nginx

However it works!

Examples:
---------
    $ cli2dlna.py -f /path/to/media/file.mp4
Assuming you have running web server on 80 port that shares your media (document_root is /path/to/media/).  
Script will notify your UPnP renderer to get media from this server (ie: http://server:80/file.mp4).  
You should have already configured own web server for file share.  

    $ cli2dlna.py -u 'http://some.other.server.net/with/file.mp4'
Script will notify your UPnP renderer to get media from this url.  
    $ cli2dlna.py -y 'https://www.youtube.com/watch?v=sOnqjkJTMaA'
Script will call youtube-dl executable to process your request.  
Therefore, you should have youtube-dl binary installed to use this option.  
By default script assumes, that youtube-dl is located in /usr/local/bin.  
You may change this behaviour by setting YOUTUBE_DL environment variable(ex: YOUTUBE_DL=/usr/bin/youtube-dl)  
youtube-dl will be executed as subprocess with -g key to get http link.  
Afterthat, this link will be sent to your UPnP renderer.  
    $ cli2dlna.py -c
Scan for remote renderers in your network.  
    $ cli2dlna.py -C
Script will send Play command to continue playing current media  
    $ cli2dlna.py -P
Script will send Pause command to pause playing current media  
    $ cli2dlna.py  -S
Script will send Stop command to stop playing current media  
    $ cli2dlna.py  -h
Script will show you usage information  

To avoid future SSDP lookups, script saves ad re-reads every time it's renderer.cache file.
