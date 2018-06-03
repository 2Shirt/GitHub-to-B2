# GitHub to Backblaze B2 #

Script to backup GitHub repo(s) to Backblaze B2.

This is the process:

* Download the specified repo to a temporary directory.
* Compress the repo using tar/gzip
* Upload the compressed archive.
* Delete the archive and repo from the temp dir.
* Repeat above steps for any additional specified repos.
* Delete the temp dir itself (if empty).

## Story ##

I wanted to apply safer shell practices to [this gist](https://gist.github.com/nilayp/a2719ca5695c1d5a56c556e89207577d) which was featured in [this blog entry](https://www.backblaze.com/blog/backing-up-github-to-cloud-storage/) by Backblaze. Work started as a fork of the gist [here](https://gist.github.com/2Shirt/6270696b857cecdf4a6d0d4f4fedeb3b) but I wanted to support backing up multiple repositories at a time. So I decided to make a full project so I could use features from the [BASH3 Boilerplate](http://bash3boilerplate.sh/).

The resulting script is likely overkill for most use-cases. It was written as an opportunity to play with the BASH3 Boilerplate.

## Changes / Improvements ##

* All variables can be passed as arguments.
* All variables are quoted for safety.
* Exit on any error, not just the specified tests.
* Clone the GitHub repo(s) using either HTTPS or SSH.
* Support backing up multiple repos.
* Authorize the B2 command line tool instead of relying on the user doing so manually.
* Recognize the B2 command line tool from the [Arch Linux](https://www.archlinux.org/) [user repository](https://aur.archlinux.org/).
  * _(It's named `backblaze-b2` instead of `b2` see [PKGBUILD](https://aur.archlinux.org/cgit/aur.git/tree/PKGBUILD?h=backblaze-b2) for details)_
* Removed optional file encryption section from source gist.
  * It wouldn't work as expected as it would encrypt the repo but then upload the non-encrypted copy instead.
  * If encryption was going to be used, I would not recommend using a symmetric cipher.
