[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/HBLL-Collection-Development/omeka-s-any-cloud/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/HBLL-Collection-Development/omeka-s-any-cloud/?branch=master)
[![Build Status](https://scrutinizer-ci.com/g/HBLL-Collection-Development/omeka-s-any-cloud/badges/build.png?b=master)](https://scrutinizer-ci.com/g/HBLL-Collection-Development/omeka-s-any-cloud/build-status/master)
[![Maintainability](https://api.codeclimate.com/v1/badges/88231b9bfaa4e0397ef9/maintainability)](https://codeclimate.com/github/HBLL-Collection-Development/omeka-s-any-cloud/maintainability)
[![StyleCI](https://github.styleci.io/repos/167904424/shield)](https://github.styleci.io/repos/167904424)
[![DOI](https://zenodo.org/badge/167904424.svg)](https://zenodo.org/badge/latestdoi/167904424)

# Any Cloud Storage (Omeka S Module)
This module allows you to store your Omeka S files on one of the following external cloud platforms rather than the local server disk:

- [Amazon S3 Storage](https://aws.amazon.com/s3/)
- [Microsoft Azure Storage](https://azure.microsoft.com/en-us/services/storage/)
- [Google Cloud Storage](https://cloud.google.com/storage/)
- [Wasabi Cloug Storage](https://wasabi.com) (uses the Amazon S3 Storage adapter)
- [DigitalOcean Spaces](https://www.digitalocean.com/products/spaces/) (uses the Amazon S3 Storage adapter)
- [Scaleway Object Storage](https://www.scaleway.com/object-storage/) (uses the Amazon S3 Storage adapter)
- [Rackspace Files](https://www.rackspace.com/cloud/files)
- [Dropbox](https://www.dropbox.com)

It uses a filesystem abstraction system called [Flysystem](http://flysystem.thephpleague.com/docs/). You can build your own adapters to use with the system if there is a cloud storage system you would like to use but is not currently available via this module.

It is recommended that once you pick an external storage service you continue using it as migrating to a different external file system is not currently supported.

## Installation and Configuration
1. Install the plugin by [downloading and unzipping the latest module](https://github.com/HBLL-Collection-Development/omeka-s-any-cloud/releases) and loading it into the `modules` directory of your Omeka S instance.
2. Enable the plugin from the Admin side of your installation under “Modules”.
3. Configure the module from the Admin side to include credentials for the cloud storage system you would like to use.

After that, when you upload media for an item, it will upload to your selected cloud service rather than to your server’s local storage.

## Known Issues
1. No migration from one cloud/filesystem to another. Pick one or manually transfer things if you decide to change services. 
2. The Rackspace Files adapter currently relies on an outdated version of the Guzzle package which causes problems authenticating to the service. See [this forum posting](https://community.rackspace.com/products/f/dedicated-hybrid-hosting-forum/8674/rackspace-public-cloud-php-opencloud-sdk-errors-due-to-outdated-certificate-authority-list/14415) for the solution which involves downloading an updated security certificate and placing it in the correct directory in the `vendor` directory. There are several issues requesting a fix but I don't know when those will be resolved. Until then, the instructions in that forum work well:
   1. Download the updated certificate authority file here: <https://curl.haxx.se/ca/cacert.pem>
   2. Replace Guzzle's certificate authority file with the updated one. It is located at: `/path/to/omeka/modules/AnyCloud/vendor/guzzle/guzzle/src/Guzzle/Http/Resources/cacert.pem`
3. There is also an authentication issue with Rackspace Files if you use Multi-Factor Authentication (MFA). MFA must be disabled on your account for this adapter to work. Hopefully both of these issues are addressed soon.

## Warning
Use this module at your own risk.

It’s always recommended to backup your files and databases and to check your archives regularly so you can roll back if needed.

## Troubleshooting
See online issues on the [module issues](https://github.com/HBLL-Collection-Development/omeka-s-any-cloud/issues) page on GitHub.

## TODO
1. - [X] Remove need for users to manually change the alias in `config/local.config.php` (v0.2.0)
2. - [X] Move all config data to a form so users can use the admin module system to enter their credentials without the need to access server files (v0.2.0)
3. - [X] Make config forms prettier and easier to use (v0.3.0)
4. - [X] Get a DOI for the software (v1.0.0)
5. - [X] Integrate a Wasabi cloud adapter (v1.1.0)
6. - [ ] Provide more detailed instructions on setting up each cloud storage system (possibly using the GitHub wiki)

## Possible Enhancements
1. - [ ] Allow migration between different cloud platforms
2. - [ ] Support [Archive Repertory](https://github.com/Daniel-KM/Omeka-S-module-ArchiveRepertory)
3. - [ ] Write tests for module
4. - [ ] Support module translation
