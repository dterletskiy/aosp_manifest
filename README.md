# Android platform


## Description

This repository contains Android platform manifest files and description how to build it.

Original Android platform manifest could be found in https://android.googlesource.com/platform/manifest/.
Manifest from some branch of this repository is used as base manifest and mentioned in ***default.xml*** first.


## Sync and build instructions.


Defining variables:

<pre>
REPO_TOOL_URL="https://storage.googleapis.com/git-repo-downloads/repo"

MANIFEST_URL="https://github.com/dterletskiy/aosp_manifest.git"
VERSION="android-12.1.0_r8-dev"
BRANCH="platform/manifest/${VERSION}"
MANIFEST_NAME="default.xml"

ARCH="arm64"
DEVICE="aosp_trout_${ARCH}"

ROOT_DIR="/mnt/dev/android/"
SOURCE_DIR="${ROOT_DIR}/source/platform/${VERSION}"
BUILD_DIR="${ROOT_DIR}/build/platform/${VERSION}"
DEPLOY_DIR="${ROOT_DIR}/deploy/platform/${VERSION}/${DEVICE}"
</pre>


Create and go to source directory:

<pre>
mkdir -p ${SOURCE_DIR}
cd ${SOURCE_DIR}
</pre>


Install repo tool:

<pre>
curl ${REPO_TOOL_URL} > repo
chmod a+x repo
</pre>


Sync Android Kernel project:

<pre>
repo --trace init --manifest-url=${MANIFEST_URL}  --manifest-name=${MANIFEST_NAME}  --manifest-branch=${BRANCH} --depth=1
repo --trace sync --current-branch --no-clone-bundle --no-tags
</pre>


Build Android Platform project:

<pre>
export OUT_DIR_COMMON_BASE=${BUILD_DIR}/..
source build/envsetup.sh
lunch ${DEVICE}
make showcommands
</pre>