---
title: "Terminal macOS tricks"
date: 2019-08-05
draft: false
tags: ["TIl"]
categories: ["til"]
mytag: "TIL"
---

:one: Config to show branch in Terminal

Open `.bash_profile` file then add:  

```shell
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

export PS1="\u@\h \[\033[32m\]\w - \$(parse_git_branch)\[\033[00m\] $ "
```

:two: Setup to use `subl` command in macOS

Run:  

```
sudo ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl /usr/local/bin/subl
```

References:  

[1][https://stackoverflow.com/questions/17333531/how-can-i-display-the-current-branch-and-folder-path-in-terminal](https://stackoverflow.com/questions/17333531/how-can-i-display-the-current-branch-and-folder-path-in-terminal)

[2][https://www.tunnelsup.com/how-to-open-sublime-text-from-the-command-line-using-mac-osx/](https://www.tunnelsup.com/how-to-open-sublime-text-from-the-command-line-using-mac-osx/)