# Unofficial ArcSight Logger API Documentation

Welcome to the unofficial API documentation for the Microfocus ArcSight Logger. This document describes all API endpoints available to users of the ArcSight Logger product.

The API itself supports only actions related to generating searches and retrieving it's results.

Only endpoints available in the RESTful API will be covered.

## Usage
There is several ways to view the documentation, depending on how you want to view it:

### Downloading the documentation
Download the required package directly from github, either from cli using:
```sh
$ git clone https://github.com/arcsight-unofficial/arcsight-logger-api-documentation
```
Or if you have internet access or a proxy server which does not allow git, download the newest release manually.
[Releases can be found here](https://github.com/arcsight-unofficial/arcsight-logger-api-documentation/releases)

### Accessing the static build of the documentation
If all you want is to quickly view the documentation without having to install the required components to run the local server, you can just open the index.html file in the root folder.

### Running a local webserver version
If you want to run a local copy of the documentation so more people have access to it, you would be required to configure node.js on your server. To find out how to install node and npm, please refer to the official documentation.

Afterwards, you can run these commands in the root directory
Installing prerequisites:
```sh
$ npm install
```
Creating a build to run:
```sh
$ node shins.js --customcss
```
Run the local webserver:
```sh
$ node arapaho
```
The documentation can then be accessed on [localhost:4567](http://localhost:4567) in your browser.