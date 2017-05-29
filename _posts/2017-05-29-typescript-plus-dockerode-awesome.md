---
layout: post
title:  "Typescript + Dockerode = awesome Docker"
date:   2017-05-29 11:37:37 +0100
categories: jekyll docker typescript dockerode
---

One thing we do at VQ is build automated tools to test and control our product.

We build Docker containers of the product for use with tools such as Protractor and Artillery.io.

Control Docker with Dockerode from Typescript, with typings it makes it a reasonably easy solution.

## Getting started

Install Dockerode to your project:

`npm install dockerode`

or

`yarn add dockerode`

Install the Dockerode Typings to your project:

`npm install -D @types/dockerode`

or

`yarn add -D @types/dockerode`

## Using

Import and use Dockerode:

```typescript
import * as Dockerode from 'dockerode';

let dockerode = new Dockerode();

let container = dockerode.getContainer('foo');
```

You then can use the typings to help find methods.

Some methods are missing types, I've contributed in the past to the project originally when it was known as dockerode-ts.

You can lookup what the Docker Remote API accepts/returns by looking at the official Docker documention for your version.

[Docker Engine API v1.29](https://docs.docker.com/engine/api/v1.29/)

## Examples

Some cool things you can do are:

### Export a containers logs

I.e. get the contents of `docker logs <container name>`

```typescript
let dockerode = new Dockerode();

let container = dockerode.getContainer('foo');

container.logs({ stdout: true, stderr: true, follow: false }, (error, stream) => {
    if (error) {
        console.error('container logs error', error);
    }

    stream.on('data', (data) => {
        console.log('container logs', data);
    });

    stream.on('error', (streamError) => {
        console.error('container logs stream error', streamError);
    });

    stream.on('end', () => {
        // Stream finished
    });
});
```

### Get files from a container

This is good if you want to grab local log files out of a container, like `docker cp`.

```typescript
let dockerode = new Dockerode();

let container = dockerode.getContainer('foo');

container.getArchive({ path: targetFolderPath }, (error: any, stream: NodeJS.ReadableStream) => {
    let writeStream = createWriteStream(`./${filename}.tar.gz`, { encoding: 'utf8' });

    if (error) {
        console.error('get archive error', error);
        writeStream.end();
        writeStream.close();
    }

    stream.on('data', (data) => {
        writeStream.write(data);
    });

    stream.on('end', () => {
        writeStream.end();
        writeStream.close();
    });
});
```

### Copy a file into a container

This is handy if you want to override config files without rebuilding the container, like `docker cp`.

```typescript
let destContainer = this.dockerode.getContainer('foo');

let configFiles = targz({}, { fromBase: true })
    .createReadStream(`./config/foo/`) as NodeJS.ReadableStream;

destContainer.putArchive(configFiles, { path: '/path/in/container/' }, (writeError, writeStream) => {
    if (writeError) {
        console.error('put archive error', writeError);
    }

    console.log('put archive finished');
});
```

### Connect a container to an existing network

When you create a container I couldn't see a way to add it to container like you do with `docker run` so here's how you can connect a container to an existing Docker network with Dockerode.

```typescript
let dockerode = new Dockerode();

let container = dockerode.getContainer('foo');

let network = this.dockerode.getNetwork('mynetwork');

network.connect({ container: container.id }, (error, result) => {
    if (error) {
        console.error('connect to network error', error);
    }

    console.log('connected to network!');
});
```