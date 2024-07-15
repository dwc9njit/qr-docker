
---

# QR Code Generator Application with Docker

This project is a Python application that generates a QR code PNG file containing a URL. The QR code can be scanned with a mobile device to navigate to the target website. This project uses Docker to ensure a consistent runtime environment.

## Features

- Generates a QR code that links to a specified URL
- Customizable QR code colors and output directory
- Dockerized for easy deployment and isolation
- Logs generation and error handling

## Setup

1. **Install Docker**:
   - Visit [Docker's official website](https://www.docker.com/get-started/) and follow the instructions to download and install Docker on your machine.

2. **Sign up for Docker**:
   - Create a Docker account if you don't already have one.

## QR Code Generation Example

This application generates a QR code that links to your GitHub homepage. For example, you can generate a QR code that points to `https://github.com/dwc9njit`.

### My QR Code Image

![QR Code](./images/QRCode_20240714230750.png)


## Building the Docker Image

To build the Docker image for this application, run the following command in the root directory of the project:

```sh
docker build -t my-qr-app .
```

This command builds a Docker image named `my-qr-app` using the Dockerfile in the current directory.

## Running the Docker Container

### Default Settings

To run the container with default settings:

```sh
docker run -d --name qr-generator my-qr-app
```

This runs your QR code generator application in detached mode (`-d`) with a container named `qr-generator`.

### Custom Settings with Environment Variables

To customize the QR code generation settings, you can set environment variables:

```sh
docker run -d --name qr-generator \
  -e QR_DATA_URL='https://your-url.com' \
  -e QR_CODE_DIR='qr_codes' \
  -e QR_CODE_FILENAME='customQR.png' \
  -e FILL_COLOR='blue' \
  -e BACK_COLOR='yellow' \
  my-qr-app
```

### Sharing a Volume for QR Code Output

To mount a host directory to the container for storing QR codes:

```sh
docker run -d --name qr-generator \
  -v /host/path/for/qr_codes:/app/qr_codes \
  my-qr-app
```

### Combined Volume Sharing and Environment Variables

A comprehensive command that configures the QR code settings and mounts volumes for QR codes:

```sh
docker run -d --name qr-generator \
  -e QR_CODE_DIR='qr_codes' \
  -e FILL_COLOR='blue' \
  -e BACK_COLOR='yellow' \
  -v /host/path/for/qr_codes:/app/qr_codes \
  my-qr-app
```

## Setting the URL from the Terminal

To set the URL for the QR code from the terminal:

```sh
docker run -v .:/app my-qr-app --url https://www.your-url.com
```

This command overrides the default URL with the specified URL for QR code generation.

## Basic Docker Commands Explained

### Building an Image

```sh
docker build -t image_name .
```

Builds a Docker image with the tag `image_name` from the Dockerfile in the current directory.

### Running a Container

```sh
docker run --name container_name image_name
```

Runs a container named `container_name` from `image_name` in the foreground.

```sh
docker run -d --name container_name image_name
```

Runs a container named `container_name` from `image_name` in detached mode.

### Listing Running Containers

```sh
docker ps
```

Shows a list of all running containers.

### Stopping a Container

```sh
docker stop container_name
```

### Removing a Container

```sh
docker rm container_name
```

### Listing Docker Images

```sh
docker images
```

Lists all Docker images available on your machine.

### Removing a Docker Image

```sh
docker rmi image_name
```

Removes a Docker image.

### Viewing Logs of a Container

```sh
docker logs container_name
```

Displays the logs from a running or stopped container.

---

These commands cover the essentials of building, running, and managing Docker containers and images, along with specific examples for your QR code generation application.