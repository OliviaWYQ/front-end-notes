## Error: Your Command Line Tools are too outdated.

Update them from Software Update in System Preferences or run:
```
  softwareupdate --all --install --force
```
If that doesn't show you any updates, run:
```
  sudo rm -rf /Library/Developer/CommandLineTools
  sudo xcode-select --install
```

## 更换为清华源

更换brew.git
```
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git
```
更换核心软件仓库（homebrew-core.git)
```
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
```
更换Home Bottles源
长期更换：
```
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```

临时更换：
```
export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles
```
## 更换为中科大源

更换brew.git
```
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
```
更换核心软件仓库（homebrew-core.git)
```
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```
更换Home cask软件仓库
```
cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
```
更换Home Bottles源
长期更换：
```
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```

临时更换：
```
export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles
```
## 重置默认源

重置brew.git
```
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git
```
重置核心软件仓库
```
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git
```
重置Homebrew cask软件仓库
```
cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
git remote set-url origin https://github.com/Homebrew/homebrew-cask
```
重置Homebrew Bottles源

```
vim ~/.bash_profile
```
注释掉bash配置文件里的有关Homebrew Bottles即可恢复官方源。 重启bash或让bash重读配置文件。
```
source ~/.bash_profile

brew update
```


## 查看是否替换成功

重启bash
```
brew config
```
