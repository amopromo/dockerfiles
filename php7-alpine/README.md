# Docker PHP-FPM 7.2 & Nginx 1.16 on Alpine Linux
Example PHP-FPM 7.2 & Nginx 1.16 setup for Docker, build on [Alpine Linux](http://www.alpinelinux.org/).
The image is only +/- 35MB large.

Repository: https://github.com/TrafeX/docker-php-nginx


* Built on the lightweight and secure Alpine Linux distribution
* Very small Docker image size (+/-35MB)
* Uses PHP 7.2 for better performance, lower cpu usage & memory footprint
* Optimized for 100 concurrent users
* Optimized to only use resources when there's traffic (by using PHP-FPM's ondemand PM)
* The servers Nginx, PHP-FPM and supervisord run under a non-privileged user (nobody) to make it more secure
* The logs of all the services are redirected to the output of the Docker container (visible with `docker logs -f <container name>`)
* Follows the KISS principle (Keep It Simple, Stupid) to make it easy to understand and adjust the image
### This is a copy from https://github.com/TrafeX/docker-php-nginx (24/4/2019)
It's open source, then i (anakinpendragon) make a copy with a new nginx version.
amopromo/nginx has nginx 1.16 , openssl 1.1.1b and brotli compression

### Breaking changes (26/01/2019)

Please note that the new builds since 26/01/2019 are exposing a different port to access Nginx.
To be able to run Nginx as a non-privileged user, the port it's running on needed
to change to a non-privileged port (above 1024).

The last build of the old version that exposed port 80 was `trafex/alpine-nginx-php7:ba1dd422`

## Usage

Start the Docker container:

    docker run -p 80:8080 trafex/alpine-nginx-php7

See the PHP info on http://localhost, or the static html page on http://localhost/test.html
