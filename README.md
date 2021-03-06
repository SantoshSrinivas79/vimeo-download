Downloads segmented audio+video from Vimeo and saves as .mp4

This script is useful for cases where youtube-dl is unable to find the master url,
for example on pages that require login or cookies.

Installation 
=======

Install requirements with `pip install -r requirements.txt`

### Installing ffmpeg

Compilation instruction: https://trac.ffmpeg.org/wiki/CompilationGuide

**For ubuntu users:**

    sudo add-apt-repository ppa:mc3man/trusty-media && sudo apt-get update 
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 8E51A6D660CD88D67D65221D90BD7EACED8E640A
    sudo apt-get install ffmpeg

(The instructions are taken from [here](http://help.ubuntu.ru/wiki/ffmpeg) - warning: Russian!)
    
**For MacOS users:**

    brew install ffmpeg



Usage
=====

To use this script, the master url needs to be manually extracted from the page:

   `python vimeo-download.py --url "http://...master.json?base64_init=1" --output <optional_name>`

`source activate env`

`python vimeo-download.py --url "https://54skyfiregce-vimeo.akamaized.net/exp=1495778158~acl=%2F166161053%2F%2A~hmac=5a10fbddc107291f4dddcca7d8e3d223268fa63f152db2125b183a2bd6c6a0e2/166161053/sep/video/529552759,529552769,529552767,529552757/master.json?base64_init=1"`

Merge audio and video

`ffmpeg -i a.mp4 -i a.mp3 -c:v copy -c:a copy output.mp4`


`source activate env`

`python vimeo-download.py --url "https://54skyfiregce-vimeo.akamaized.net/exp=1495778158~acl=%2F166161053%2F%2A~hmac=5a10fbddc107291f4dddcca7d8e3d223268fa63f152db2125b183a2bd6c6a0e2/166161053/sep/video/529552759,529552769,529552767,529552757/master.json?base64_init=1"`

Merge audio and video

`ffmpeg -i a.mp4 -i a.mp3 -c:v copy -c:a copy output.mp4`


To get the master url:

   1. Open the network tab in the inspector
   2. Find the url of a request to the `master.json` file
   3. Run the script with the url as argument

You can download multiple files in parallel with GNU Parallel:

   `parallel -a master-files.txt python vimeo-download.py --url "{}"`

Where `master-files.txt` contains a list of master URLs


Acknowledgements
=======

Code merges the following gists:

- https://gist.github.com/alexeygrigorev/a1bc540925054b71e1a7268e50ad55cd
- https://gist.github.com/tayiorbeii/d78c7e4b338b031ce8090b30b395a46f
- https://gist.github.com/paschoaletto/7f65b7e36b76ccde9fe52b74b62ab9df

Alternatives
============

For a more convenient experience use youtube-dl ( http://rg3.github.io/youtube-dl/ ) if youtube-dl is able to find the url
