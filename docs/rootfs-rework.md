# Rootfs rework

Reference: PeronGH/linux-gaokun-buildbot at a7aac4ae6a04f42fe4adf46cea60cfa4258b1bbf.
Adapted its bootstrap, Fedora image configuration, RPM templates, static monitor
configuration and image finalization. See upstream commits ca5d2010 and 0656fd81
for the RPM/environment and firmware/boot-hook changes.

Both distributions keep an ESP and a single ext4 root partition. The kernel
remains pinned to 0a95cd00a3eb3a43f04746d2b4c6c9f1c7acf485, whose bonded-DSI
restoration resolved half-screen corruption in the user's test.

Fedora now uses Plasma Setup to create the first account; there is no preset
user login. Fedora 44 uses Plasma Login Manager. The image retains explicit
NetworkManager-tui installation, required service enablement, SELinux selection
and offline labeling with -m for the Ubuntu build host. KDE uses a system-wide
KWin output configuration for the internal DSI-1 panel (right rotation, 200%
scale). Users can override it in Plasma Display Configuration. Rotation on the
greeter, first-run wizard and user desktop must still be validated on hardware.
Plymouth is disabled and the boot menu editor remains enabled.

Firmware RPMs supplement Fedora's qcom/atheros packages with model-specific
files only. RPMs must be rebuilt for this candidate; older artifacts with the
same kernel SHA still carry the superseded firmware and install hooks.

The workflow preserves exact kernel SHA checks and opt-in publishing. Successful
assembly checks boot payloads, KDE components, service enablement and RPM
provides, but cannot prove Plasma Login, first-run setup, networking or suspend
works on hardware.

Ubuntu keeps its existing account/bootstrap configuration and GNOME monitors.xml;
shared device assets and per-device identity cleanup are applied there as well.
Historical manual build guides describe the pre-migration workflow.
