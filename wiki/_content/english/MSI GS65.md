    *   [2.1 Webcam is not detected](#Webcam_is_not_detected)
    *   [4.4 System freeze](#System_freeze)
Using the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") it is possible to rebuild the kernel using this patch which add the mapping for the wifi on kernel 4.17.6
From d4156c9f4dfb872da1e512cfdf6aa0648c839210 Mon Sep 17 00:00:00 2001
 repos/core-x86_64/0005-Add-wifi-support.patch | 10 ++++++++++
 repos/core-x86_64/PKGBUILD                    |  7 ++++++-
 2 files changed, 16 insertions(+), 1 deletion(-)
 create mode 100644 repos/core-x86_64/0005-Add-wifi-support.patch
diff --git a/repos/core-x86_64/0005-Add-wifi-support.patch b/repos/core-x86_64/0005-Add-wifi-support.patch
+++ b/repos/core-x86_64/0005-Add-wifi-support.patch