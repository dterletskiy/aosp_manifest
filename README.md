# aosp_manifest

This repository contains xml files with original android manifest and othen manifests for extending aosp.

Commands and sequence:

   'mkdir -p android/platform/android-12.1.0_r8-dev'

   'cd android/platform/android-12.1.0_r8-dev'

   'curl https://storage.googleapis.com/git-repo-downloads/repo > repo'

   'chmod a+x repo'

   './repo init -u git@github.com:dterletskiy/aosp_manifest.git/ -m default.xml -b platform/manifest/android-12.1.0_r8-dev'

   './repo sync --current-branch --no-clone-bundle --no-tags'

