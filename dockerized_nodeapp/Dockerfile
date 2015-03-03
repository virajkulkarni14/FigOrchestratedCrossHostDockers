# Dockerizing Nodejs: Dockerfile for building Nodejs images with Express framework app 
# Base image is phusion/passenger-nodejs
FROM phusion/passenger-nodejs:0.9.15

MAINTAINER Viraj Kulkarni <mail@virajkulkarni.me>

# Set correct environment variables.
ENV HOME /root

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Equivalent to: export DEBIAN_FRONTEND="noninteractive" which means no questions asked on apt-get install
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install gcc make build-essential

# Bundle app source
COPY . /src
# Install app dependencies
RUN cd /src/src; npm install

EXPOSE  8080
CMD ["node", "/src/app.js"]

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*