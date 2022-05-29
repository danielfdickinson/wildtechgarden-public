---
imageFeatured: /assets/images/cover/PiBoardOfficialCase.jpg
slug: armshorian
aliases:
    - /projects/defunct/armshorian/
    - /develop-design/arm-development/armshorian/
    - /devel/armshorian/
author: Daniel F. Dickinson
date: '2020-01-18T19:22:00+00:00'
publishDate: '2020-01-18T19:22:00+00:00'
title: 'REMOVED: Armshorian'
description: "Generating real Debian images for armel devices"
tags:
    - arm-devel
    - armel
    - armhf
    - devel
    - docs
    - firmware
    - linux
    - rootfs-images
    - virtualization
toc: true
weight: 15000
featuredImageAlt: "Photo of a Raspberry Pi 2 in an official case with the top removed and held in the palm of an adult human"
articleContentClassExtra: armshorian-article-content
---

## REMOVED Fork of Rpi-Distro/pi-gen

**WARNING**: Due to <https://bugs.launchpad.net/qemu/+bug/1805913> images built on non-arm hosts are broken!

* As I am, once again, late to the party and there are sufficient projects for most needs (and I have enough other things to work on) I am abandoning this fork.
* The code no longer exists in a public repository.
* For various use cases you can see there are other options:

| Use-Case                                              | Suggested Project                                                                           |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Modified raspbian images                              | Modify <https://github.com/RPi-Distro/pi-gen>                                               |
| Build Debian ARM images (especially for Pi 0/1/2/3/4) | Modify <https://github.com/drtyhlpr/rpi23-gen-image>                                        |
| Debian on SBC                                         | Modify FreedomBox’s [Freedom-Maker](https://salsa.debian.org/freedombox-team/freedom-maker) |

## Dependencies

armshorian-gen runs on Debian based operating systems. Currently it is only
supported on either Debian Buster or Ubuntu Xenial and is known to have issues
building on earlier releases of these systems. On other Linux distributions it
may be possible to use the Docker build described below.

To install the required dependencies for armshorian-gen you should run:

{{< highlight sh >}}apt-get install coreutils quilt parted qemu-user-static debootstrap zerofree zip \
dosfstools bsdtar libcap2-bin grep rsync xz-utils file git curl
{{< /highlight >}}

The file depends contains a list of tools needed. The format of this
package is \<tool>\[:\<debian-package>].

## Config

Upon execution, build.sh will source the file config in the current
working directory. This bash shell fragment is intended to set needed
environment variables.

The following environment variables are supported:

* IMG_NAME **required** (Default: unset) The name of the image to build with the current stage directories. Setting IMG_NAME=Armshorian is logical for an unmodified cshoredaniel/armshorian- gen build, but you should use something else for a customized version. Export files in stages may add suffixes to IMG_NAME.

* APT_PROXY (Default: unset) If you require the use of an apt proxy, set it here. This proxy setting will not be included in the image, making it safe to use an apt-cacher or similar package for development.

  * If you have Docker installed, you can set up a local apt caching proxy to like speed up subsequent builds like this:

     ```bash
     docker-compose up -d echo 'APT_PROXY=http://172.17.0.1:3142' >> config
     ```

* BASE_DIR (Default: location of build.sh) **CAUTION**: Currently, changing this value will probably break build.sh
  * Top-level directory for armshorian-gen. Contains stage directories, build scripts, and by default both work and deployment directories.
* WORK_DIR (Default: "$BASE_DIR/work") Directory in which armshorian-gen builds the target system. This value can be changed if you have a suitably large, fast storage location for stages to be built and cached. Note, WORK_DIR stores a complete copy of the target system for each build stage, amounting to tens of gigabytes in the case of Raspbian.
  * **CAUTION**: If your working directory is on an NTFS partition you probably won’t be able to build. Make sure this is a proper Linux filesystem.
* DEPLOY_DIR (Default: "$BASE_DIR/deploy") Output directory for target system images and NOOBS bundles.
* DEPLOY_ZIP (Default: 1) Setting to 0 will deploy the actual image (.img) instead of a zipped image (.zip).
* USE_QEMU (Default: "0") Setting to ‘1’ enables the QEMU mode - creating an image that can be mounted via QEMU for an emulated environment. These images include “-qemu” in the image file name.
* LOCALE_DEFAULT (Default: “en_GB.UTF-8” ) Default system locale.
* LOCALE_GEN_DEFAULT (Default: “en_GB.UTF-8 UTF-8” ) List of locales to generate each separated by a comma and a space (in that order). Note a locale is typically of the form \<lang>_\<COUNTRY>.\<encoding> \<encoding> (e.g. en_GB.UTF-8 UTF-8). See stage0/01-locale/00-debconf for a list of available locales.
* TARGET_HOSTNAME (Default: “raspberrypi”; Raspshorian: “raspshorian”; Armshorian: “armshorian” )
  * Sets the hostname to the specified value.
* KEYBOARD_KEYMAP (Default: “gb”; Raspshorian & Armshorian: “us” ) Default keyboard keymap.
  * To get the current value from a running system, run debconf-show keyboard-configuration and look at the keyboard-configuration/xkb-keymap value.
* KEYBOARD_LAYOUT (Default: “English (UK)"; Raspshorian & Armshorian: “English (US)” ) Default keyboard layout.
  * To get the current value from a running system, run debconf-show keyboard-configuration and look at the keyboard-configuration/variant value.
* TIMEZONE_DEFAULT (Default: “Europe/London”, Raspshorian & Armshorian: “America/Toronto” ) Default keyboard layout.
  * To get the current value from a running system, look in /etc/timezone.
* FIRST_USER_NAME (Default: “pi”; Raspshorian: “rcshore”; Armshorian: “acshore” )
  * Username for the first user
* FIRST_USER_PASS (Default: “raspberry”; Raspshorian: “raspshorian-default”; Armshorian: “armshorian-default”)
  * Password for the first user
* WPA_ESSID, WPA_PASSWORD and WPA_COUNTRY (Default: unset)
  * **NB**: Not used by Raspshorian or Armshorian
  * If these are set, they are use to configure wpa_supplicant.conf, so that the Raspberry Pi can automatically connect to a wifi network on first boot. If WPA_ESSID is set and WPA_PASSWORD is unset an unprotected wifi network will be configured. If set, WPA_PASSWORD must be between 8 and 63 characters.
* ENABLE_SSH (Default: 0)
  * Setting to 1 will enable ssh server for remote log in. Note that if you are using a common password such as the defaults there is a high risk of attackers taking over you Raspberry Pi.
* PUBKEY_SSH_FIRST_USER (Default: unset)
  * Setting this to a value will make that value the contents of the FIRST_USER_NAME’s ~/.ssh/authorized_keys. Obviously the value should therefore be a valid authorized_keys file. Note that this does not automatically enable SSH.
* PUBKEY_ONLY_SSH (Default: 0)
  * Setting to 1 will disable password authentication for SSH and enable public key authentication. Note that if SSH is not enabled this will take effect when SSH becomes enabled.
* STAGE_LIST (Default: stage*; Raspshorian: raspshorian-stage*; Armshorian: armshorian-stage*)
  * If set, then instead of working through the numeric stages in order, this list will be followed. For example setting to "stage0 stage1 mystage stage2" will run the contents of mystage before stage2. Note that quotes are needed around the list. An absolute or relative path can be given for stages outside the armshorian-gen directory.
* stageX_EXPORT_LIST (Default: based on presence of EXPORT_IMAGE and/or EXPORT_NOOBS in stageX directory (currently stage2, stage4, and stage5) )
  * If set, then instead of determining images to export based on EXPORT_IMAGE and/or EXPORT_NOOBS being present in a particular directory the images to export for a particular stage is based on that stage’s stageX_EXPORT_LIST. Only stages with a stageX_EXPORT_LIST (e.g. stage2_EXPORT_LIST) are determined this way. All other stages use the default method (presence of EXPORT_IMAGE and/or EXPORT_NOOBS). For stages with a stageX_EXPORT_LIST, the contents of EXPORT_LIST are expected to be directory names in the repo directory. In addition, files with each directory in EXPORT_LIST translated to upper case and dashes (-) converted to underscores (_) in the stage’s directory are sourced before generating the image. (e.g. an ‘export-image’ in the stage2_EXPORT_LIST first sources stage2/EXPORT_IMAGE and then generates an images using the export-image directory, which is the same behaviour as the old default behaviour.
* HEADLESS (Default: 0)
  * Sets serial console as primary console and HDMI console as secondary.
  * A simple example for building Raspbian:

    ```bash
    IMG_NAME='Raspbian'
     ```

    The config file can also be specified on the command line as an argument the build.sh or build-docker.sh scripts.

    ```bash
    ./build.sh -c myconfig
    ```

     This is parsed after config so can be used to override values set there.

## How the build process works

The following process is followed to build images:

* Loop through all of the stage directories in alphanumeric order
* Move on to the next directory if this stage directory contains a file called “SKIP”
* Run the script prerun.sh which is generally just used to copy the build directory between stages.
* In each stage directory loop through each subdirectory and then run each of the install scripts it contains, again in alphanumeric order. These need to be named with a two digit padded number at the beginning. There are a number of different files and directories which can be used to control different parts of the build process:
  * **00-run.sh** - A unix shell script. Needs to be made executable for it to run.
  * **00-run-chroot.sh** - A unix shell script which will be run in the chroot of the image build directory. Needs to be made executable for it to run.
  * **00-debconf** - Contents of this file are passed to debconf-set-selections to configure things like locale, etc.
  * **00-packages** - A list of packages to install. Can have more than one, space separated, per line.
  * **00-packages-nr** - As 00-packages, except these will be installed using the --no-install-recommends -y parameters to apt-get.
  * **00-patches** - A directory containing patch files to be applied, using quilt. If a file named ‘EDIT’ is present in the directory, the build process will be interrupted with a bash session, allowing an opportunity to create/revise the patches.
* If the stage directory contains files called “EXPORT_NOOBS” or “EXPORT_IMAGE” or has a corresponding stageX_EXPORT_LIST, then add this stage to a list of images to generate
* Generate the images for any stages that have specified them

It is recommended to examine build.sh for finer details.

## Docker Build

Docker can be used to perform the build inside a container. This partially isolates
the build from the host system, and allows using the script on non-debian based
systems (e.g. Fedora Linux). The isolation is not complete due to the need to use
some kernel level services for arm emulation (binfmt) and loop devices (losetup).

To build:

```bash
vi config # Edit your config file. See above.
./build-docker.sh
```

If everything goes well, your finished image will be in the deploy/ folder.
You can then remove the build container with docker rm -v pigen_work

If something breaks along the line, you can edit the corresponding scripts, and
continue:

```bash
CONTINUE=1 ./build-docker.sh
```

To examine the container after a failure you can enter a shell within it using:

```bash
sudo docker run -it --privileged --volumes-from=pigen_work armshorian-gen/bin/bash
```

After successful build, the build container is by default removed. This may be undesired when making incremental changes to a customized build. To prevent the build script from removing the container add

```bash
PRESERVE_CONTAINER=1 ./build-docker.sh
```

There is a possibility that even when running from a docker container, the
installation of qemu-user-static will silently fail when building the image
because binfmt-support *must be enabled on the underlying kernel*. An easy
fix is to ensure binfmt-support is installed on the host machine before
starting the ./build-docker.sh script (or using your own docker build
solution).

## Stage Anatomy

### Raspshorian Stage Overview

The build of Raspshorian is divided up into several stages for logical clarity
and modularity. This causes some initial complexity, but it simplifies
maintenance and allows for easier customization.

* **Stage 0** - bootstrap. The primary purpose of this stage is to create a usable filesystem. This is accomplished largely through the use of debootstrap, which creates a minimal filesystem suitable for use as a base.tgz on Debian systems. This stage also configures apt settings and installs raspberrypi-bootloader which is missed by debootstrap. The minimal core is installed but not configured, and the system will not quite boot yet.
* **Stage 1** - truly minimal system. This stage makes the system bootable by installing system files like /etc/fstab, configures the bootloader, makes the network operable, and creates the first user (besides root which is not directly available). At this stage the system should boot to a local console from which you have the means to perform basic tasks needed to configure and install the system. This is almost as minimal as a system can possibly get, and its arguably not really usable yet in a traditional sense yet. Still, if you want minimal, this is minimal and the rest you could reasonably do yourself as sysadmin.
* **Stage 2** - minimal system. This stage produces the Raspshorian-Minimal image. It installs some optimized memory functions, sets timezone and charmap defaults, installs fake-hwclock, ntp, and other basics for managing the hardware. It also creates necessary groups and gives the primary user access to sudo and the standard console hardware permission groups. It also includes OpenSSH. Wireless is not included in the CLI only environment.
* **Stage 3** - lite system. This stage produces the Raspshorian-Lite image. It is close to a stock Debian command line only system with the ‘standard’ packages installed as well as OpenSSH and Python3 (for Ansible).
* **Stage 4** - Normal Raspshorian desktop system. Here’s where you get the base desktop system with X11 and WindowMaker, web browser, email client etc. (WindowMaker was selected as the least demanding complete desktop environment). Note the desktop environment configuration is a work in progress. Adds network-manager and wireless (wpasupplicant).
* **Stage 5** - The Raspshorian Full image. Adds LibreOffice, Firefox-ESR, and printer and scanner support. (This is a separate stage because these are rather large). The image should still fit on a 4GB SD card.

### Raspbian Stage Overview

The build of Raspbian is divided up into several stages for logical clarity
and modularity. This causes some initial complexity, but it simplifies
maintenance and allows for easier customization.

* **Stage 0** - bootstrap. The primary purpose of this stage is to create a usable filesystem. This is accomplished largely through the use of debootstrap, which creates a minimal filesystem suitable for use as a base.tgz on Debian systems. This stage also configures apt settings and installs raspberrypi-bootloader which is missed by debootstrap. The minimal core is installed but not configured, and the system will not quite boot yet.
* **Stage 1** - truly minimal system. This stage makes the system bootable by installing system files like /etc/fstab, configures the bootloader, makes the network operable, and installs packages like raspi-config. At this stage the system should boot to a local console from which you have the means to perform basic tasks needed to configure and install the system. This is as minimal as a system can possibly get, and its arguably not really usable yet in a traditional sense yet. Still, if you want minimal, this is minimal and the rest you could reasonably do yourself as sysadmin.
* **Stage 2** - lite system. This stage produces the Raspbian-Lite image. It installs some optimized memory functions, sets timezone and charmap defaults, installs fake-hwclock and ntp, wifi and bluetooth support, dphys-swapfile, and other basics for managing the hardware. It also creates necessary groups and gives the pi user access to sudo and the standard console hardware permission groups. There are a few development tools here that may not make a whole lot of sense on a minimal system. These tools include basic Python and Lua packages as well as the build-essential package. They are lumped right in with more essential packages presently, though they need not be with armshorian-gen. They are understandable for Raspbian’s target audience, but if you were looking for something between truly minimal and Raspbian-Lite, here’s where you start trimming.
* **Stage 3** - desktop system. Here’s where you get the full desktop system with X11 and LXDE, web browsers, git for development, Raspbian custom UI enhancements, etc. This is a base desktop system, with some development tools installed.
* **Stage 4** - Normal Raspbian image. System meant to fit on a 4GB card. This is the stage that installs most things that make Raspbian friendly to new users like system documentation.
* **Stage 5** - The Raspbian Full image. More development tools, an email client, learning tools like Scratch, specialized packages like sonic-pi, office productivity, etc.

### Stage specification

If you wish to build up to a specified stage (such as building up to stage 2
for a lite system), place an empty file named SKIP in each of the ./stage
directories you wish not to include.

Then add an empty file named SKIP_IMAGES to ./stage4 and ./stage5 (if building up to stage 2) or
to ./stage2 (if building a minimal system).

{{< highlight sh >}}# Example for building a lite system
echo "IMG_NAME='Raspbian'" > config
touch ./stage3/SKIP ./stage4/SKIP ./stage5/SKIP
touch ./stage4/SKIP_IMAGES ./stage5/SKIP_IMAGES
sudo ./build.sh # or ./build-docker.sh
{{< /highlight >}}

If you wish to build further configurations upon (for example) the lite
system, you can also delete the contents of ./stage3 and ./stage4 and
replace with your own contents in the same format.

## Skipping stages to speed up development

If you’re working on a specific stage the recommended development process is as
follows:

* Add a file called SKIP_IMAGES into the directories containing EXPORT_* files
(currently stage2, stage4 and stage5)
* Add SKIP files to the stages you don’t want to build. For example, if you’re
basing your image on the lite image you would add these to stages 3, 4 and 5.
* Run build.sh to build all stages
* Add SKIP files to the earlier successfully built stages
* Modify the last stage
* Rebuild just the last stage using sudo CLEAN=1 ./build.sh
* Once you’re happy with the image you can remove the SKIP_IMAGES files and
export your image to test

## Troubleshooting

### 64 Bit Systems

Please note there is currently an issue when compiling with a 64 Bit OS. See <https://github.com/RPi-Distro/pi-gen/issues/271>

#### binfmt_misc

Linux is able execute binaries from other architectures, meaning that it should be
possible to make use of armshorian-gen on an x86_64 system, even though it will be running
ARM binaries. This requires support from the [binfmt_misc](https://en.wikipedia.org/wiki/Binfmt_misc)
kernel module.

You may see the following error:

{{< highlight sh >}}update-binfmts: warning: Couldn't load the binfmt_misc module.
{{< /highlight >}}

To resolve this, ensure that the following files are available (install them if necessary):

{{< highlight sh >}}/lib/modules/$(uname -r)/kernel/fs/binfmt_misc.ko
/usr/bin/qemu-arm-static
{{< /highlight >}}

You may also need to load the module by hand - run modprobe binfmt_misc.

> *© 2020 Daniel F. Dickinson and Released under a BSD Three Clause License*
