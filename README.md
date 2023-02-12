# aosp_manifest

This repository contains xml files with original android kernel manifest and othen manifests for extending kernel.

Commands and sequence:

   'mkdir -p android/kernel/common-android14-6.1-dev'

   'cd android/kernel/common-android14-6.1-dev'

   'curl https://storage.googleapis.com/git-repo-downloads/repo > repo'

   'chmod a+x repo'

   './repo init -u git@github.com:dterletskiy/aosp_manifest.git/ -m default.xml -b kernel/manifest/common-android14-6.1-dev'

   './repo sync --current-branch --no-clone-bundle --no-tags'

