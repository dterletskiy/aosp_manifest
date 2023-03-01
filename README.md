# aosp_manifest

This repository contains xml files with original android manifest and othen manifests for extending aosp.

Sync and build instructions.


Defining variables:

<pre>
REPO_TOOL_URL="https://storage.googleapis.com/git-repo-downloads/repo"

MANIFEST_URL="https://github.com/dterletskiy/aosp_manifest.git"
VERSION="android-12.1.0_r8-dev"
BRANCH="platform/manifest/${VERSION}"
MANIFEST_NAME="default.xml"

ARCH="aarch64"
DEVICE="virtual_device_${ARCH}"
BUILD_CONFIG="//common-modules/virtual-device:${DEVICE}"

ROOT_DIR="/mnt/dev/android/"
SOURCE_DIR="${ROOT_DIR}/source/platform/${VERSION}"
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
@TDA: to do
</pre>