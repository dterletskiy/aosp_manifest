# aosp_manifest

This repository contains xml files with original android manifest and othen manifests for extending aosp.

Commands and sequence:

   'cd <android_root>'

   'curl https://storage.googleapis.com/git-repo-downloads/repo > repo'

   'chmod a+x repo'

   './repo init -u git@github.com:dterletskiy/aosp_manifest.git/ -m default.xml -b <branch_name>'

   './repo sync --current-branch --no-clone-bundle --no-tags'

