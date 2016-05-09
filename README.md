# jenkins-data

This is a starter data image for jenkins at BBD. It contains 
  * pre-configured jobs (including a job generator template), 
  * project matrix security with an admin/admin user, 
  * maven 3.3.9 and git (from debian base)

Plugins and jenkins version are handled from the master jenkins image (see sdoxsee/jenkins).

Job source is stored in a private github repository and requires a private key for ssh.

## Setup

OSX users need to install `gtar` since OSX's `tar` doesn't let you create with explicit owner/group. Explicit ownership is important since jenkins runs with the jenkins user and ownership isn't easily set using docker (see [ref](https://github.com/docker/docker/issues/6119)). Install with homebrew:
```
brew install gnu-tar
```
Then follow the post install instructions to add the following to your `~/.bash_profile` to make the `tar` command actually use `gtar`:
```
# for using gtar (from homebrew) as tar
export PATH="/usr/local/opt/gnu-tar/libexec/gnubin:$PATH"
export MANPATH="/usr/local/opt/gnu-tar/libexec/gnuman:$MANPATH"
```
For more info on installing a custom tar application on OSX see [ref](http://superuser.com/questions/318809/linux-os-x-tar-incompatibility-tarballs-created-on-os-x-give-errors-when-unt/688231#688231)

## How To

1. Copy `/var/jenkins_home` from container to your host (under a `jenkins_home` directory)? Run `docker cp <container-id>:/var/jenkins_home .`
2. Create a new tar.gz from your updated `jenkins_home`? Run `tar-jenkins_home.sh`
3. Allow pulls from private BBD github repo? Add the private ssh key to the root of this project as `build-machine.id_rsa` (note that it is in .gitignore)






