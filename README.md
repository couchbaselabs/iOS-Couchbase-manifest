# Building With Repo

## Get Repo

    $ curl http://android.git.kernel.org/repo > ~/bin/repo
    $ chmod a+x ~/bin/repo

## Clone the Manifest

    $ mkdir iOS-Couchbase-repo
    $ cd iOS-Couchbase-repo
    $ repo init -u git@github.com:couchbaselabs/iOS-Couchbase-manifest.git
    $ repo sync

## Build

See the instructions in the `CouchbaseMobile` directory.