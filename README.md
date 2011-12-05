# Building And Contributing To Couchbase Mobile For iOS

This repository contains the "manifest" for Couchbase Mobile for iOS, which is simply an XML file that instructs the "repo" tool where to find the multiple Git repositories containing the source code, and where to send patches to the Gerrit tool. If you want to build Couchbase Mobile from source, or make contributions, these instructions will get you started.

## Get The "Repo" Tool

[Repo][1] is a tool developed for the Android build system for managing sets of related Git repositories and submitting patches [for review][2]. It's a single file that's easy to install:

    $ curl http://git-repo.googlecode.com/files/repo-1.12 > ~/bin/repo
    $ chmod a+x ~/bin/repo

(This assumes `~/bin` already exists and is in your shell search path. If not, you can add it, or you can download `repo` somewhere else that's already in your `$PATH`.)

Repo's help system works like git's. Type `repo help` to see a list of commands, and `repo help command` to get help on a particular command. (For some reason you have to be inside a directory managed by repo to be able to use help.)

## Clone the Manifest And Couchbase Projects

    $ mkdir iOS-Couchbase
    $ cd iOS-Couchbase
    $ repo init -u git://github.com/couchbaselabs/iOS-Couchbase-manifest.git
    $ repo sync

## Build

See the instructions in `CouchbaseMobile/README.md`.

To pull in changes from upstream, use the command `repo sync`, then rebuild.

## Contribute Improvements

[“Good for you! You've decided to improve open-source software.”][3]

Important! Changes have to be submitted through the [Gerrit code-review system][2]. This is different from the Github workflow of forks and patch-requests that you may be more used to. (But hey, it beats [explosive bolts][3].)

### Before making changes:

    repo start MyBranchName --all

This will create new branches named `MyBranchName` in each git repository. Pick a branch name that reminds you of what you're working on, e.g. `optimizeTwiddling` or `fixBug1234`.

The command `repo branch` will list all current branches known to repo. `repo checkout` will check out a branch across all repositories.

### Submitting your changes:

Commit your changes to the local git repositories as usual. If you've made changes in multiple repositories, remember to commit in each one! The command `repo status` is helpful to show uncommitted changes in all git repositories.

When you're ready to submit:

1. Enter `repo upload` to upload your patches to Gerrit.
2. The command will output the URL of the new code review page; go to that URL.
3. If necessary, sign into Gerrit, with the same email address that appears in your git commits. If that email address doesn't support OpenID, then log in using an address that does, such as any Google or Yahoo! account, then go to Settings > Identities to add your Git email address.
4. On the patch page, enter the email address of someone you want to review your patch, into the field next to the "Add Reviewer" button, then press the button.

### Fixing your patches:

The reviewer(s) might find bugs or style issues that they want you to fix. If so, they'll make comments in the Gerrit web UI, which will be emailed to you. It's easy to upload a fixed patch:

1. Remember to check out the correct repo branch, if you have more than one.
2. Make the changes to the source.
3. Build and test to make sure the changes work!
4. Use `git amend` to update your prior commit with the new changes. DO NOT commit a second time on top of the first one, or you'll confuse Gerrit (it will think you're submitting two different changes.)
5. `repo upload` again, to upload the new patch-set. This won't create a new web page on Gerrit, just add content to the existing one.
6. You don't need to notify the reviewers; Gerrit will do that. Then they'll look at your new patch and either approve it or ask for more changes.

[1]: http://source.android.com/source/version-control.html
[2]: http://review.couchbase.org/
[3]: http://youtu.be/PePSQtc5YPU?t=6m15s
