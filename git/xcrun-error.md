# xcrun Error with Invalid Active Developer Path

After I updated my mac, I received an error like the following when you're running any command on macOS:

```jsx
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools),
missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
```

This indicates that the Command Line Tools for XCode are not properly installed (they may have been broken by a recent macOS update). Reinstall them:

```jsx
xcode-select --install
```

If that fails, try resetting the path of the Command Line Tools:

```jsx
sudo xcode-select --reset
```

If resetting the path didn't help, you can download the latest Command Line Tools for XCode at [Xcode download](https://developer.apple.com/xcode/)
