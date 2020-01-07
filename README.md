# Why this image?

By design, it is better not to add [parcel](https://parceljs.org/) to your project as a dependency.

# Running

Install the dependencies of your project:

```shell
$ docker run --rm \
  -v $(pwd):/app -w /app -v node_modules:/app/node_modules \
  dmitryrck/node-alpine-parcel \
  npm install
```

Build your project:

```shell
$ docker run --rm \
  -v $(pwd):/app -w /app -v node_modules:/app/node_modules \
  dmitryrck/node-alpine-parcel \
  parcel build src/index.html --public-url /static -d /app/public/static
```

In production, you can combine that two commands:

```shell
$ docker run --rm \
  -v $(pwd):/app -w /app -v node_modules:/app/node_modules \
  dmitryrck/node-alpine-parcel \
  sh -c "npm install && parcel build src/index.html --public-url /static -d /app/public/static"
```
