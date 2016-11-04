- [Set XCode FileMerge as default difftool and mergetool] (https://gist.github.com/kylefox/4512777)
```
# Tell system when Xcode utilities live:
sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer

# Set "opendiff" as the default mergetool globally:
git config --global merge.tool opendiff

# Set "opendiff" as the default difftool globally:
git config --global diff.tool opendiff
```
