# Why this image?

By design, it is better not to add [parcel](https://parceljs.org/) to your app as a dependency.

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
