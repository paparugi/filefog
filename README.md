#`var FileFog = require('filefog')`

[![Circle CI](https://circleci.com/gh/filefog/filefog.svg?style=svg)](https://circleci.com/gh/filefog/filefog)

There are many cloud storage options for consumers. However each provider has their own API and API design philosophy, making it harder for developers to easily integrate their applications.

The idea behind FileFog is to provide a single consistent, promise-based API for developers to access user uploaded data, without having to worry about differing OAuth implementations, base urls or data parsing.

The FileFog philosophy is as follows:

- __Don't reinvent the wheel__ - if a native library is available for NodeJS, use it. All we need  to do then is wrap the required methods to create a consistent user experience, and let the API designers themselves deal with most fo the implementation details.
- __Avoid Callback Hell__ - Javascript and most libraries built on-top of it heavily make use of callbacks. While this is perfectly fine for some, I prefer the Promise design pattern for its reliability, simplicity and synchronous feel when working with pseudo-filesystems.

# WARNING
Please note that this package is under heavy development, and the unified API may change unexpectedly. Once the API is stable, a version 1.0 will be released on NPM.

# Providers
Initally FileFog will be released with only support for the following popular Cloud Services.

- Google
- SkyDrive
- Dropbox
- Box.net
- Local filesystem
- Microsoft Azure Storage

Providers for the following Cloud Services are also planned:

- Amazon S3
- Bittorrent Sync
- AnyCloud
- FTP
- WebDAV


# Usage

    var filefog = require('filefog')

# Quick Start
    var filefog = require('filefog')

    //This registration only needs to be done once.
    filefog.use('dropbox', require('filefog-dropbox'), {client_key : '...',client_secret : '...'});;


    //create a dropbox provider and client using previously saved access_tokens
    var dropboxProvider = filefog.provider("dropbox")
    //call dropboxProvider.oAuthGetAuthorizeUrl() if you do not have access_tokens already.
    //dropboxProvider.oAuthGetAuthorizeUrl()

    dropboxClient = dropboxProvider.getClienta({
        access_token: '...',
        refresh_token: '...'
    })
    .then(function (client) {
        return client.getFolderInformation();
    }).then(function (response) {
        //Dropbox folder metadata, in a standardized format.
    })

# Documentation
    The docs are currently out of date, and as this library is underdevelopment and the API is not yet stable, this won't change for the forseeable future.

# TODO's
- Docs
- Search method
- Update method
- state - built-in state antiforgery token support.


# Supported filefog_options
    These are a list of commonly supported filefog options.
    {Boolean|true} transform - determines if the raw response from the storage service is transformed to a filefog standardized format.
    {Boolean|true} include_raw - include the raw response in the transformed response
    {Boolean|true} auto_paginate - auto_paginate the responses if required
    {String|null} root_identifier - set the root_identifier to namespace all filefog operations to a specific folder.
