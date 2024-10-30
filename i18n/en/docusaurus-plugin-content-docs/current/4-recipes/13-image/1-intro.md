---
sidebar_position: 1
---

# About Images

Docker images are lightweight, executable software packages that contain everything needed to run a piece of software or application—code, runtime environment, libraries, environment variables, and configuration files. Docker images are the foundation for building Docker containers, and each image is immutable; when you run an image, it becomes a container.

Docker images have the following characteristics:

1. **Layered Storage**: Docker images are composed of multiple layers, with each layer representing a step in the image building process. When modifying an image, you only need to add new layers without changing existing ones, making image distribution and updates highly efficient.

2. **Sharing and Reuse**: Multiple images can share the same layers. If different images use the same base layers, these layers only need to be stored once on the machine, saving space and improving efficiency.

3. **Immutability**: Once created, an image's content cannot be changed. All modifications to containers (such as adding new files or changing existing ones) occur in the container's writable layer without affecting the underlying image.

4. **Version Control and Rollback**: Docker images can be version-controlled through tags, making it easy to manage and roll back to specific versions.

5. **Lightweight**: Since images load layers on demand, they are lightweight, start quickly, and are easy to scale and distribute.

6. **Portability**: Images contain all dependencies needed to run applications and can be executed on any platform that supports Docker, ensuring consistent runtime environments.

Docker images are typically built from a base image and customized through a Dockerfile (a text file containing custom instructions). These custom images can be stored locally or uploaded to public or private image registries (such as Docker Hub) for others to use. Docker images can be pulled from repositories to local machines using the `docker pull` command, and containers can be started from images using the `docker run` command.

# About coScene Image Registry

The coScene platform provides a private image registry, eliminating the need for users to set up their own. Users can quickly upload existing images to the coScene image registry, enabling immediate use of these images on the coScene platform to build business processes and improve development efficiency. The coScene image registry is supported in features such as [Automation](../12-action/1-quickstart.md) and [Batch Testing](../8-regression/1-intro.md).
