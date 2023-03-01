# Android kernel

## Description

This repository contains Android kernel manifest files and description how to build it.

Original Android kernel manifest could be found in https://android.googlesource.com/kernel/manifest/.
Manifest from some branch of this repository is used as base manifest and mentioned in ***default.xml*** first.


## Sync and build instructions.


Defining variables:

<pre>
REPO_TOOL_URL="https://storage.googleapis.com/git-repo-downloads/repo"

MANIFEST_URL="https://github.com/dterletskiy/aosp_manifest.git"
VERSION="common-android14-6.1-dev"
BRANCH="kernel/manifest/${VERSION}"
MANIFEST_NAME="default.xml"

ARCH="aarch64"
DEVICE="virtual_device_${ARCH}"
BUILD_CONFIG="//common-modules/virtual-device:${DEVICE}"

ROOT_DIR="/mnt/dev/android/"
SOURCE_DIR="${ROOT_DIR}/source/kernel/${VERSION}"
DEPLOY_DIR="${ROOT_DIR}/deploy/kernel/${VERSION}/${DEVICE}"
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


Build Android Kernel project using bazel:

<pre>
tools/bazel run ${BUILD_CONFIG}_dist -- --dist_dir=${DEPLOY_DIR}
</pre>


Shutdown bazel server (to avoid some bugs and side effects):

<pre>
tools/bazel shutdown
</pre>
