# Useful Tips for Mac OSX Developers

## Git
- [Set XCode FileMerge as default difftool and mergetool] (https://gist.github.com/kylefox/4512777)
```
# Tell system when Xcode utilities live:
sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer

# Set "opendiff" as the default mergetool globally:
git config --global merge.tool opendiff

# Set "opendiff" as the default difftool globally:
git config --global diff.tool opendiff
```

- Show what files are checked in 
```
git log --name-only
```

- Create your alias
```
[alias]
    ls = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate
    ll = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]" --decorate --numstat
    ls-file = log --name-only
    diffc = diff --cached
```

## Sublime
- [Link sublime in command line](http://stackoverflow.com/questions/16199581/opening-sublime-text-on-command-line-as-subl-on-mac-os)
```
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl
```

## Reading Materials for Advanced JavaScript Developer
- [Getting Started with Redux](https://egghead.io/courses/getting-started-with-redux)
- [Building React Applications with Idiomatic Redux](https://egghead.io/courses/building-react-applications-with-idiomatic-redux)
