# Docker Trusted Registry - Default Demo Runbook
This file describes the default step by step runbook to do a demo of Docker Trusted Registry

## Version 
This runbook was tested with Docker Trusted Registry 2.4.1 (last checked 9th of January 2017).

## Preparation steps

To be able to do this demo you need to do the following configuration steps with your Docker Trusted Registry installation upfront:

* TBD

You could also use the following configuration script to create a default configuration for demo.

## Before doing the demo

Before you plan to do the demo make sure the following is configured correctly:

* Config 1
* Config 2
* Config 3

## Runbook

1. Administration

Login as admin user:

* Show Organizations and Users. Explain the connection to UCP
* Show the Repositories and explan namespaces and repository names.
* 

2. Image Management

Login as a restricted user:

* Show the existing Repositories and explain namespaces and repository names.
* Create a new repository by using the mytweet app (Link to Dockerfile). Use a description with more details for your application. Name it user/mytweetapp. Don't show advanced setting and scan on push should be disabled at this stage. Use a private repo so you need to login before pushing the image.
* Build the local mytweetapp 1.0 version if you didn't already by using the command docker build -t mytweetapp . inside the folder of the application.
* tag it with the name of the repo by using the command: docker tag mytweetapp:1.0 <mydtr>/<myuser>/mytweetapp:1.0
* Login to your dtr by using the command docker login yourdtrname
* Explain that now all layers are uploaded because none of them did exists before.
* Push version 1.0 of the application to the DTR by using the command docker push <mydtr>/<user>/mytweetapp:1.0
* Update the index.html and the title to show how to also create a new version of the application.
* Build the mytweetapp version 2.0 by using the docker command docker build -t mytweetapp:2.0
* tag it with the name of the repo by using the command: docker tag mytweetapp:1.0 <mydtr>/<myuser>/mytweetapp:2.0
* push it as well to the dtr by using the command docker push <mydtr>/<user>/mytweetapp:2.0
* Show and explain that now you only the layer with the index.hml file is uploaded. All other layers do already exist so DTR is using pointers to combine the old and new version of the image.

2. High Available and Redundant System
3. Efficiency (Cache Image, Garbage Collection)
4. Built-in access control
5. Security Scanning (Binary Level)
6. Image Signing (Docker Content Trust)
7. Automatic Image Promotion
8. Immutable Repositories
9. Webhooks
10. API for Integration & Configuration Management



