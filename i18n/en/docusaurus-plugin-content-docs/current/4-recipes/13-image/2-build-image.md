---
sidebar_position: 2
---

# Preparing Images

Using Docker to build your own images.

## Prerequisites

Docker must be installed and running on your machine. If you need to install Docker, please refer to the corresponding [installation documentation](https://docs.docker.com/engine/install/).

## Preparing Image Files

Create a new folder containing the dockerfile and related test code. Below is a demonstration using a simple Python file named hello.py and a dockerfile.

- Example dockerfile

```bash
FROM python:3.12 AS builder

# copy files
COPY hello.py /usr/src/app/

WORKDIR /usr/src/app

# set command/entrypoint, adapt to fit your needs
CMD ["python", "hello.py"]
```

- Example test code

```python
if __name__ == "__main__":
    print("Hello, World!")
```

## Building the Image

Let's assume the image name is `cr.coscene.cn/coscene/helloworld` with the tag `latest`

```bash
docker build -f dockerfile -t cr.coscene.cn/coscene/helloword:latest .
```

If you need cross-compilation support for different platforms, please check the [documentation](https://docs.docker.com/build/building/multi-platform/)

## Running the Image

After the image is built, we can run it to verify the code functionality.

```bash
docker run cr.coscene.cn/coscene/helloword:latest
```

Check the output - if the image was built correctly, it should show our expected result.

![](./img/build-image-1.png)
