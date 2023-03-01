# aosp_manifest

This repository contains xml files with original android kernel manifest and othen manifests for extending kernel.

Sync and build instructions.


Defining variables:

<pre>
REPO_TOOL_URL="https://storage.googleapis.com/git-repo-downloads/repo"

MANIFEST_URL="https://android.googlesource.com/kernel/manifest"
BRANCH="common-android14-6.1"
MANIFEST_NAME="default.xml"

ARCH="aarch64"
DEVICE="virtual_device_${ARCH}"
BUILD_CONFIG="//common-modules/virtual-device:${DEVICE}"

ROOT_DIR="/mnt/dev/android/"
SOURCE_DIR="${ROOT_DIR}/source/kernel/${BRANCH}"
DEPLOY_DIR="${ROOT_DIR}/deploy/kernel/${BRANCH}/${DEVICE}"
</pre>


Install repo tool:

<pre>
mkdir -p ${SOURCE_DIR}
cd ${SOURCE_DIR}

curl ${REPO_TOOL_URL} > repo
chmod a+x repo
</pre>


Sync Android Kernel project:

<pre>
repo --trace init -u ${MANIFEST_URL} -m ${MANIFEST_NAME} -b ${BRANCH} --depth=1
repo --trace sync -c -j4
</pre>


Build Android Kernel project using bazel:

<pre>
tools/bazel run ${BUILD_CONFIG}_dist -- --dist_dir=${DEPLOY_DIR}
</pre>


Shutdown bazel server (to avoid some bugs and side effects):

<pre>
tools/bazel shutdown
</pre>
