# MacOS tips and tricks

## Show/hide the hidden files

### Temporary keyboard shortcut to toggle

++cmd+shift+"."++

### Always show or hide

```shell
# To show
defaults write com.apple.finder AppleShowAllFiles TRUE

# To hide
defaults write com.apple.finder AppleShowAllFiles FALSE

# Restart Finder after that
killall Finder
```

## Add space to dock

```shell
defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="small-spacer-tile";}'; killall Dock
```

## Screenshot

!!! info "Restart `SystemUIServer` after below changes"

    ```shell
    killall SystemUIServer
    ```

### Change default location

```shell
defaults write com.apple.screencapture location ~/Desktop/screenshots
```

### Change default name

```shell
defaults write com.apple.screencapture name "name"
```

## Delete all executable files in command line

```shell
find . -maxdepth 1 -perm -111 -delete
```

## List all apps installed from App Store

```shell
find /Applications -path '*Contents/_MASReceipt/receipt' -maxdepth 4 -print | sed 's#.app/Contents/_MASReceipt/receipt#.app#g; s#/Applications/##'
```

## Remove shadow from window screenshot

```shell
defaults write com.apple.screencapture disable-shadow -bool true ; killall SystemUIServer
```