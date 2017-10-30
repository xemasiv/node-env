Just created this https://hub.docker.com/r/xemasiv/node-env/

### Summary:

It's a modified version of TailorBrands' version, with the following changes:

* Base image is now pulled from official node:latest image, making the node easily interchangeable with older versions by just editing a single line.
* Image is now inclusive with node-gyp dependencies for rebuilding libraries, so installed npm packages (thru Dockerfile, or real-time dev/prod) will build flawlessly
* Image is also inclusive of 'sharp' npm package, npm-installed as a global library
* Added tweaks that:
  * Allowed installation of global package in NPM (thru chown & sudo)
  * Allowed requiring of globally installed packages (thru ~/.bashrc fix)

### Contents:

* node:latest @ v8.8.1; 5.4.2
* vips @ vips-8.5.5
* gcc & g++ for node-gyp
* npm install --global of 'sharp' library
* chown to allow that npm --global install
* ~/.bashrc fix to allow requiring of globally installed packages

### Setup

* `docker pull xemasiv/node-env`
* `docker run -it -d xemasiv/node-env`
* `docker container ls` --> to get the container name
* `docker attach <container_name>`

### Testing (now logged in as root):

* `node -v && npm -v && vips -v`
* `node` --> takes you to node cli
* `require('sharp')` --> should return the sharp function itself.

### Usage

* attach your project directory as a docker volume.
* expose a port to make your project accessible from the host machine & outside world.
* this gives you an environment where vips and 'sharp' library is already accessible.

### Credits:

* Check the Dockerfile for the sources and the things you can modify.
