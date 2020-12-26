# ansible-open-multistream
Quickly set up your server to forward your RTMP stream to multiple RTMP or RTMPS targets

## Alternatives
* Use [muesli/prism](https://github.com/muesli/prism) instead for an easier way to restream from RTMP to RTMP
  * has no support for RTMPS as a target (planned afaik)
  * has no support for people watching directly from your server (afaik)

## Configuration
Works for me(tm) on a fresh Debian 10 installation. Might work on other distributions.
* Add your host(s) to `hosts`
* Run `ansible-playbook -i hosts setup.yml`
* Change settings in `group_vars/all`
  * Change the streaming key
  * Set some features to either "enabled" or anything else to disable them (e.g. "disabled")
  * (optional) Add your RTMPS (take note of the S) streaming targets to the array, it is pre-filled for Instagram as a target but you may choose your own
    * You may enlarge the array by copying it while keeping `description` and `local_port` unique
  * By default, it is possible to watch your stream directly from your restream-server by opening `rtmp://SERVER_IP/zuschauen` in VLC or other RTMP-capable video-players
* Run `ansible-playbook -i hosts configure.yml` to apply the configuration you set in `group_vars/all` and (re)start the services

## Streaming to your server
* Add `rtmp://SERVER_IP/RESTREAM_KEY` to your custom streaming target in OBS. 
  * Note: Leave the "Streaming key" field in OBS empty and include it in the URL instead as shown
