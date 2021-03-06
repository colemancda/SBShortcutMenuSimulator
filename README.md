# SBShortcutMenuSimulator

`SBShortcutMenuSimulator` is a tweak for the iPhone Simulator that allows you to simulate the new `UIApplicationShortcutItem` API for iPhone with 3D Touch enabled.

## Requirements

- Xcode 7 GM or later, set as your default version of Xcode

## Installation

**Note:** Installing SBShortcutMenuSimulator makes a minor change to your Xcode installation, which will invalidate Xcode's code signature. Uninstalling (as described below) will restore Xcode to its original state.

``` sh
git clone https://github.com/DeskConnect/SBShortcutMenuSimulator.git
cd SBShortcutMenuSimulator
make

PLIST_PATH="$(xcrun --sdk iphonesimulator --show-sdk-path)/System/Library/LaunchDaemons/com.apple.SpringBoard.plist"
cp "${PLIST_PATH}" com.apple.SpringBoard.plist.bak
plutil -replace EnvironmentVariables -json "{\"DYLD_INSERT_LIBRARIES\": \"${PWD}/SBShortcutMenuSimulator.dylib\"}" "${PLIST_PATH}"
killall SpringBoard
```

## Usage

To show an app's quick action menu, send the app's bundle identifier over TCP to port 8000. For example, running this command will show the shortcut menu for Calendar.

``` sh
echo 'com.apple.mobilecal' | ncat 127.0.0.1 8000
```

<img src="https://raw.githubusercontent.com/DeskConnect/SBShortcutMenuSimulator/screenshot/Shortcuts.png" width="326" height="592"></img>

## Uninstallation

``` sh
cp "com.apple.SpringBoard.plist.bak" "$(xcrun --sdk iphonesimulator --show-sdk-path)/System/Library/LaunchDaemons/com.apple.SpringBoard.plist"
killall SpringBoard
```

## License

SBShortcutMenuSimulator is available under the MIT license. See the LICENSE file for more info.
