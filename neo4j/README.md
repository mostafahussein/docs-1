<!--

********************************************************************************

WARNING:

    DO NOT EDIT "neo4j/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "neo4j/" combined with a set of templates)

********************************************************************************

-->

# Supported tags and respective `Dockerfile` links

-	[`3.5.8`, `3.5`, `latest`](https://github.com/neo4j/docker-neo4j-publish/blob/53d8c355498de280a7b6ad4b9259bb8f132a1839/3.5.8/community/Dockerfile)
-	[`3.5.8-enterprise`, `3.5-enterprise`, `enterprise`](https://github.com/neo4j/docker-neo4j-publish/blob/53d8c355498de280a7b6ad4b9259bb8f132a1839/3.5.8/enterprise/Dockerfile)
-	[`3.5.7`](https://github.com/neo4j/docker-neo4j-publish/blob/ffc4f941cc9a301ad41d1649aa021c0fc727919b/3.5.7/community/Dockerfile)
-	[`3.5.7-enterprise`](https://github.com/neo4j/docker-neo4j-publish/blob/ffc4f941cc9a301ad41d1649aa021c0fc727919b/3.5.7/enterprise/Dockerfile)
-	[`3.5.6`](https://github.com/neo4j/docker-neo4j-publish/blob/c3d38b9d9fbe589282d4974ce66af1d3f3da0c22/3.5.6/community/Dockerfile)
-	[`3.5.6-enterprise`](https://github.com/neo4j/docker-neo4j-publish/blob/c3d38b9d9fbe589282d4974ce66af1d3f3da0c22/3.5.6/enterprise/Dockerfile)
-	[`3.4.14`, `3.4`](https://github.com/neo4j/docker-neo4j-publish/blob/e3ddc2d97443a058c19cd5997d8c0df48c1956a9/3.4.14/community/Dockerfile)
-	[`3.4.14-enterprise`, `3.4-enterprise`](https://github.com/neo4j/docker-neo4j-publish/blob/e3ddc2d97443a058c19cd5997d8c0df48c1956a9/3.4.14/enterprise/Dockerfile)

# Quick reference

-	**Where to get help**:  
	[Stack Overflow](http://stackoverflow.com/questions/tagged/neo4j)

-	**Where to file issues**:  
	[https://github.com/neo4j/docker-neo4j/issues](https://github.com/neo4j/docker-neo4j/issues)

-	**Maintained by**:  
	[Neo4j](https://github.com/neo4j/docker-neo4j)

-	**Supported architectures**: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
	[`amd64`](https://hub.docker.com/r/amd64/neo4j/)

-	**Published image artifact details**:  
	[repo-info repo's `repos/neo4j/` directory](https://github.com/docker-library/repo-info/blob/master/repos/neo4j) ([history](https://github.com/docker-library/repo-info/commits/master/repos/neo4j))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images PRs with label `library/neo4j`](https://github.com/docker-library/official-images/pulls?q=label%3Alibrary%2Fneo4j)  
	[official-images repo's `library/neo4j` file](https://github.com/docker-library/official-images/blob/master/library/neo4j) ([history](https://github.com/docker-library/official-images/commits/master/library/neo4j))

-	**Source of this description**:  
	[docs repo's `neo4j/` directory](https://github.com/docker-library/docs/tree/master/neo4j) ([history](https://github.com/docker-library/docs/commits/master/neo4j))

# What is neo4j?

Neo4j is the world's leading graph database, with native graph storage and processing. You can learn more [here](http://neo4j.com/developer).

![logo](https://raw.githubusercontent.com/docker-library/docs/2289fb3b561c63750032ac74ff65034c0e486072/neo4j/logo.png)

# How to use this image

You can start a Neo4j container like this:

```console
docker run \
    --publish=7474:7474 --publish=7687:7687 \
    --volume=$HOME/neo4j/data:/data \
    neo4j
```

which allows you to access neo4j through your browser at [http://localhost:7474](http://localhost:7474).

This binds two ports (`7474` and `7687`) for HTTP and Bolt access to the Neo4j API. A volume is bound to `/data` to allow the database to be persisted outside the container.

By default, this requires you to login with `neo4j/neo4j` and change the password. You can, for development purposes, disable authentication by passing `--env=NEO4J_AUTH=none` to docker run.

# Documentation

For more examples and complete documentation please go to our manual [here](https://neo4j.com/docs/operations-manual/current/docker/introduction/).

# Releases after 3.4.14 and 3.5.6

As of 11th June 2019 all new Neo4j Docker images will be released with a base image of debian-slim instead of alpine linux. This was prompted by [security concerns](https://github.com/docker-library/openjdk/issues/320), which caused the docker maintainers to pull the alpine images from the official `openjdk` images.

Older Neo4j images have already been released with `openjdk:8-jre-alpine` as the base image. This means our old images can no longer be listed as "supported" on docker hub, although **they are still available for download**.

In addition to the supported tags, we also have these legacy images of Neo4j available through docker hub:

-	`3.5.5`, `3.5.5-enterprise` and earlier patches
-	`3.4.13`, `3.4.13-enterprise` and earlier patches
-	`3.3`, `3.3-enterprise`, `3.3.9`, `3.3.9-enterprise` and earlier patches
-	`3.2`, `3.2-enterprise`, `3.2.14`, `3.2.14-enterprise` and earlier patches

A complete list of all available Neo4j images can be found here: https://github.com/neo4j/docker-neo4j-publish/tree/master

## Migrating from Alpine Linux to Debian Slim

If you have created a custom Dockerfile based off a `neo4j` image, the main change to be aware of is that debian uses the `aptitude` package manager instead of `apk`. In most cases you can just replace uses of `apk` with `apt`, but be aware that not all packages in `apk` may be available or have the same name.

Alpine Linux provide a more complete comparison on their documentation page:

https://wiki.alpinelinux.org/wiki/Comparison_with_other_distros

## Changes to file permission requirements

Some users have [raised concerns](https://github.com/neo4j/docker-neo4j/issues/130) that the Neo4j image changes file permissions on the host machine.

By default, Neo4j runs as the user `neo4j` who only exists in the container, not on the host. That means that it's hard to set up mount folders on the host which this new user has write permissions for. We have updated the error messaging with advice about how to fix file permission errors. We also introduced writability checks and reduced the amount of file permission changes the image will perform. This has been found to interfere with some Kubernetes setups, so is currently an opt-in feature.

To enforce stricter file permissions checking you can pass this environment variable to the container:

`--env SECURE_FILE_PERMISSIONS=yes`

# License

View [licensing information](https://neo4j.com/licensing) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `neo4j/` directory](https://github.com/docker-library/repo-info/tree/master/repos/neo4j).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
