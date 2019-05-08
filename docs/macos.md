# macOS

## Create Flash Installer

On `shop2` there are `.tar` files for some macOS installers. On a mac system,
first use finder to browse to `shop2` then `share`. Once you open `share`, it
will be mounted at `/Volumes/share`. Then you can extract one of them from a
terminal like this:

```text
sudo tar -xf /Volumes/share/macos/install_os_x_mavericks.tar.bz2 -C /Applications/
```

When `tar` finishes (it can take a while), you should see the installer in
Applications. For the next step, see this page on Apple's website:

<https://support.apple.com/en-us/HT201372>

## Mac Startup Keys

<https://support.apple.com/en-us/HT201255>

## Apple Hardware Test

<https://github.com/upekkha/AppleHardwareTest>
