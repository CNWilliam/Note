# config的三个作用域

## 缺省等同于local

```git
git config --local "local只对某个仓库有效"
git config --global "global对当前用户所有仓库有效"
git config --system "system"对系统所有登录的用户有效
```



## 显示config的配置，加 --list

```
git config --list -- local
git config --list --global
git config --list --system
```



