---
title: "Convert the macOS Beta Installer to an ISO Image"
date: "2021-06-13"
categories: 
  - "post"
tags: 
  - "macos"
---

As a cautious explorer, you may want to try out the newly released Developer Preview of macOS Monterey while keeping your production installation safe; it is a preferable choice to run the beta in a VM.

However, since most hypervisors recognize only an ISO image, and not the “Install macOS Beta.app” bundle provided by Apple, as the installation source, it is necessary to convert the app bundle to a disk image.

The process can be done within the following steps, which essentially (a) create an empty disk image, (b) prepare it as an installation media (as you’d do with a physical drive), and (c) convert it to the ISO format.

1. Create an empty DMG image:  
    `hdiutil create -o /tmp/macOS12 -size 12000m -volname macOS12 -layout SPUD -fs HFS+J`
2. Mount the DMG:  
    `hdiutil attach /tmp/macos12.dmg -noverify -mountpoint /Volumes/macos12`
3. Write to the DMG with `createinstallmedia`  
    `sudo /Applications/Install\ macOS\ 12\ Beta.app/Contents/Resources/createinstallmedia --volume /Volumes/macos12 --nointeraction`
4. **\[Easy to forget but necessary for proceeding\]** Unmount the DMG:  
    `hdiutil detach /Volumes/macos12`
5. Convert DMG to CDR:  
    `hdiutil convert /tmp/macos12.dmg -format UDTO -o ~/Downloads/macos12.cdr`
6. Convert (essentially rename) CDR to ISO:  
    `mv ~/Downloads/macos12.cdr ~/Downloads/macos12.iso`

You may want to free disk space by removing the temporary disk image created during the creation process: `rm /tmp/macos12.dmg` or moving it to another location for archiving.

References:

[`hdiutil(1)`](https://ss64.com/osx/hdiutil.html)

See also:

- [How to Convert a MacOS Installer to ISO](https://osxdaily.com/2020/07/20/how-convert-macos-installer-iso/)
- [How to run macOS Monterey (12) Beta in VMware Fusion – EUCSE Blog](https://blog.eucse.com/how-to-run-macos-monterey-12-beta-in-vmware-fusion/)
