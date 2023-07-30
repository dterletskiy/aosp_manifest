# Android u-boot


## Description

This repository contains Android u-boot manifest files and description how to build it.

Original u-boot manifest was not found in https://android.googlesource.com/.

But it is possible to find Android u-boot manifest in https://ci.android.com/:

- Go to https://ci.android.com/builds/branches/aosp_u-boot-mainline/grid?
- Choose the u-boot build (date and configuration), which you would like to build locally and open it's artifacts.
- The is ***manifest_xyz.xml*** inside just opened artifacts, where ***xyz*** would be the opened CI/CD job number ( e.g. 9671786 )
- Exactly this manifest could be used as the base manifest to sync u-boot source code and required environment.



## Sync and build instructions.


Defining variables:

<pre>
REPO_TOOL_URL="https://storage.googleapis.com/git-repo-downloads/repo"

MANIFEST_URL="https://github.com/dterletskiy/aosp_manifest.git"
VERSION="u-boot-mainline-master"
BRANCH="u-boot/manifest/${VERSION}"
MANIFEST_NAME="default.xml"

ARCH="aarch64"
DEVICE="qemu_${ARCH}"
BUILD_CONFIG="//u-boot:${DEVICE}"

ROOT_DIR="/mnt/dev/android/"
SOURCE_DIR="${ROOT_DIR}/source/u-boot/${VERSION}"
DEPLOY_DIR="${ROOT_DIR}/deploy/u-boot/${VERSION}/${DEVICE}"
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


Sync Android U-BOOT project:

<pre>
repo --trace init --manifest-url=${MANIFEST_URL}  --manifest-name=${MANIFEST_NAME}  --manifest-branch=${BRANCH} --depth=1
repo --trace sync --current-branch --no-clone-bundle --no-tags
</pre>


Build Android U-BOOT project using bazel:

<pre>
tools/bazel run ${BUILD_CONFIG}_dist -- --dist_dir=${DEPLOY_DIR}
</pre>


Shutdown bazel server (to avoid some bugs and side effects):

<pre>
tools/bazel shutdown
</pre>
