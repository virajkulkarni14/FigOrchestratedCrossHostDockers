# Dockerizing MongoDB: Dockerfile for building MongoDB images
# Base image is phusion/baseimage
FROM phusion/baseimage:0.9.16

MAINTAINER Viraj Kulkarni <mail@virajkulkarni.me>

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Equivalent to: export DEBIAN_FRONTEND="noninteractive" which means no questions asked on apt-get install
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get update --fix-missing
RUN apt-get update --fix-missing
RUN apt-get install -y curl

# Installation:
# Import MongoDB public GPG key AND create a MongoDB list file
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | tee /etc/apt/sources.list.d/10gen.list

# Update apt-get sources AND install MongoDB
RUN \
	apt-get update -y && \
	apt-get install mongodb-10gen
	#apt-get update && \
	#apt-get install -y mongodb-org && \
	#apt-get install -y mongodb-org-server

RUN sed -i 's/dbpath =\/var\/lib\/mongodb/dbpath =\/data\/db/' /etc/mongodb.conf

# Create the MongoDB data directory
RUN mkdir -p /data/db

VOLUME ["/data/db"]

# Expose port 27017 from the container to the host
EXPOSE 27017

# Set usr/bin/mongod as the dockerized entry-point application
ENTRYPOINT ["usr/bin/mongod"]
#ENTRYPOINT ["mongod", "-f", "/data/mongodb.conf"]

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*