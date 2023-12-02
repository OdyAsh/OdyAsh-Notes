
we have two options for streaming media (like videos): cloud or on-premise streaming. Check details [here](https://www.liquidweb.com/blog/cloud-vs-on-premise-video-hosting/#:~:text=On%2Dpremises%20video%20hosting%20can,only%20using%20the%20necessary%20resources.). 

For cloud options, there are free (YouTube, Dailymotion, Vimeo) and premium services. More details [here](https://kinsta.com/blog/video-hosting/). 

Additionally, we can use "rclone" with a cloud storage service (e.g., Google Drive) and a streamer (e.g., Jellyfin) as a large/cheap storage option for media. More details [here](https://techperplexed.blogspot.com/2017/04/) and [here](https://github.com/kelinger/OmniStream).

For on-premise option, we can connect a self-hosted server to a streamer (e.g., Jellyfin, Plex, etc.). To do so, we need a:
* web server
* streaming software (e.g., ffmpeg)
* a reliable content delivery network (CDN) (e.g., Nginx, Amazon CloudFront)
* A media player (e.g., VLC, HTML5 video player, etc.)
Detailed steps [here](https://www.vplayed.com/blog/video-streaming-server/#:~:text=How%20Do%20You%20Set%20Up%20a%20Video%20Streaming%20Server%20in%205%20Steps%3F).

