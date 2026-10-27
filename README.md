# Installing GridLinkOS Desktop

The desktop app is the same GridLinkOS you get in the browser, plus the Haunt FM Discord bot
host. Installers are published on the public releases page:

**https://github.com/AnotherJulia/GridLinkOS-releases/releases/latest**

The app is **not code-signed or notarized** by Apple or Microsoft, so both operating systems
show a warning the first time you open it. The steps below get past it. After the first
install, updates download and install from inside the app and need none of this.

| | Windows | macOS |
| --- | --- | --- |
| Download | `…_x64-setup.exe` | `…_aarch64.dmg` |
| Needs | Windows 10 or 11, 64-bit | Apple Silicon (M1 or newer) |
| First-run workaround | Click through SmartScreen | Remove the quarantine flag (`xattr`) |

There is no Intel Mac build.

## Windows

1. Open the [latest release](https://github.com/AnotherJulia/GridLinkOS-releases/releases/latest)
   and download the file ending in **`_x64-setup.exe`** from **Assets**. Ignore the `.msi`
   and `.sig` files, and `latest.json` (that one is for the auto-updater).
2. Run the downloaded installer.
3. If Windows shows **"Windows protected your PC"**, click **More info**, then **Run anyway**.
   This appears because the installer is unsigned, not because anything is wrong with it.
4. Follow the installer. It installs for your user account and does not need administrator
   rights.
5. Start **GridLinkOS** from the Start menu.

### Updating

Nothing to do. On launch the app checks for a newer version and shows a "GRIDLINK//SYSTEM
UPDATE" screen if there is one. It downloads, installs and restarts by itself. You can also
check by hand under **Settings → Updates**.

### If you have two copies

If the Start menu or **Settings → Apps → Installed apps** lists both **GridLinkOS** and
**GridLinkOS Hong Kong Edition**, the old one (**GridLinkOS**) is a leftover. Uninstall
**GridLinkOS**, keep **Hong Kong Edition**, and use the Hong Kong Edition shortcut from then on.
Your data lives in your GridLinkOS account, not in the install, so nothing is lost.

## macOS

1. Open the [latest release](https://github.com/AnotherJulia/GridLinkOS-releases/releases/latest)
   and download the file ending in **`_aarch64.dmg`** from **Assets**.
2. Open the DMG and drag the app into **Applications**. Eject the DMG.
3. **Before the first launch**, open **Terminal** and run:

   ```sh
   xattr -dr com.apple.quarantine "/Applications/GridLinkOS Hong Kong Edition.app"
   ```

   If you still have an older install, the app is named `GridLinkOS.app` instead:

   ```sh
   xattr -dr com.apple.quarantine /Applications/GridLinkOS.app
   ```

   Nothing prints when it works.
4. Open the app from Applications or Launchpad.

### Why the `xattr` step is needed

Files downloaded in a browser get a "quarantine" flag. Gatekeeper checks quarantined apps for
an Apple signature and notarization, and GridLinkOS has neither, so macOS refuses to open it
("is damaged and can't be opened" or "cannot be verified"). The command removes that flag from
this one app. It does not turn off Gatekeeper for anything else.

If you opened the app before running the command and macOS blocked it, just run the command
afterwards and open it again.

### Updating

Same as Windows: the app updates itself on launch, or under **Settings → Updates**. Updates
the app downloads itself are not quarantined, so you only run `xattr` for the first install.

If you reinstall from a freshly downloaded DMG later, run the `xattr` command again.
