# Why this image?

By design, it is better not to add [parcel](https://parceljs.org/) to your app as a dependency.

This image is _optimized_ for production, it basically makes you reduce the size of the image you have to download and let you skip the step of installing parcel.

Other images:

| Image | Features | Parcel Installed? | Size |
| ----- | -------- | ----------------- | ---- |
| [dmitryrck/ruby](https://github.com/dmitryrck/ruby-ci) | Ruby, Nodejs, Google Chrome, and Parcel | 🗸 | 4.0GB |
| [node](https://hub.docker.com/_/node) | Official docker image for Nodejs, no Parcel installed | × | 1.8GB |
| [node:alpine](https://hub.docker.com/_/node) | Official docker image for Nodejs using Alpine Linux no Parcel installed | × | 111M |
| This image | Uses `node:alpine` to install Parcel | 🗸 | 213M |

# Running

Install the dependencies of your app:

```shell
$ docker run --rm \
  -v $(pwd):/app -w /app -v node_modules:/app/node_modules \
  dmitryrck/node-alpine-parcel \
  npm install
```

Start your app:

```shell
$ docker run --rm \
  -v $(pwd):/app -w /app -v node_modules:/app/node_modules \
  -p 1234 -p 1235 \
  dmitryrck/node-alpine-parcel \
  parcel --no-autoinstall --port 1234 --hmr-port 1235 src/index.html
```

Build your app:

```shell
$ docker run --rm \
  -v $(pwd):/app -w /app -v node_modules:/app/node_modules \
  dmitryrck/node-alpine-parcel \
  parcel build src/index.html --public-url /static -d /app/public/static
```

Debuging your app:

```shell
$ docker run --rm \
  -v $(pwd):/app -w /app -v node_modules:/app/node_modules \
  dmitryrck/node-alpine-parcel \
  -it \
  sh
```

It will leave you in a shell within `/app` (binding for your app). Remember that anything you do there outside `/app` will be deleted when you type `exit`.

# Building

In production, you can install and build your app with one command:

```shell
$ docker run --rm \
  -v $(pwd):/app -w /app -v node_modules:/app/node_modules \
  dmitryrck/node-alpine-parcel \
  sh -c "npm install && parcel build src/index.html --public-url /static -d /app/public/static"
```

If your goal is to create _ephemeral_ deployments you can just copy `public/static` or clean up:

```shell
$ docker rmi dmitryrck/node-alpine-parcel
$ docker volume rm node_modules
```
