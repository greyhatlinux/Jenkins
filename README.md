# Jenkins and Automation

The tool for automating most of the parts of a software development process. It eases the road to build, test and deploy. It lays the bridge from development server to the production server with least human intervention, eliminating possible errors and delays.

## System SetUp
    You must have the following setup correctly installed, up and running : 

1. Base Operating System - Any Linux Distro
2. Docker Setup 
3. Jenkins with GitHub Plugin 

## The Desired WorkFlow : 

We wish to automate the process from code commit uptil code deployment on the production server.
   
As soon as the developer commits his changes in local git, the webhooks associated to post-commit executes, it triggers two events at a time. 

First, the commit auto runs the git push command, so that the local system with the developer and the remote system in the cloud remains in sync. After this, the hook triggers the (one of the 3) Jenkins Jobs to pull the code from GitHub. 

Jenkins then spins a docker container with fresh config to test the new code on a whole isolated environment. Here, code is tested against various parameters. This is the quality assurance test.


After the test, if the code passes the quality assurance test, it becomes deployment ready. The test container is destroyed, and the code is copied to the document root of the webserver. 

* This document root is mounted as an additional volume to the production server. Due to this, as soon as the code is copied, it gets into real-production env.