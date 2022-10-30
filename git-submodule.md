```sh

git clone --recursive git@github.com:zzjHub520/cpp-demo1.git

git submodule add -b <branch> <url> <path>

git submodule add -b v1.10.0 https://github.com/gabime/spdlog.git ./3rdparty/spdlog

git submodule add https://github.com/gabime/spdlog.git ./thirdparty/spdlog
```





## 一.子模块使用场景

当你在一个Git 项目上工作时，你需要在其中使用另外一个Git 项目，它是一个第三方开发的Git 库或者是你独立开发，但是在多个父项目中使用的。这个情况下一个常见的问题产生了：你想将两个项目单独处理但是又需要在其中一个中使用另外一个。

## 二.子模块(submodule)概念的引入

在Git 中你可以用子模块submodule来管理这些项目，submodule允许你将一个Git 仓库当作另外一个Git 仓库的子目录。这允许你克隆另外一个仓库到你的项目中并且保持你的提交相对独立。

## 三.添加子模块

此文中统一将远程项目https://github.com/cain/cain-test.git克隆到本地test文件夹。

git命令：

```sh
git submodule add 子项目url 子项目存放到本地的文件夹名
$ git submodule add https://github.com/cain/cain-test.git test
```

以上命令，将远程项目https://github.com/cain/cain-test.git克隆到本地`test`文件下。 

添加子模块后运行`git status`, 可以看到目录有增加1个文件.gitmodules, 这个文件用来保存子模块的信息。

```sh
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   .gitmodules
    new file:   test
```

## 四.查看子模块 

```sh
$ git submodule
 e23e823d3f51f5ebd731a68da05ad0371c3a0231 test (heads/master)
```

## 五.更新子模块 

#### ■ 更新项目内子模块到最新版本

```sh
$ git submodule update
```

#### ■ 更新子模块为远程项目的最新版本

```sh
$ git submodule update --remote
```

## 六.克隆包含子模块的项目 

克隆包含子模块的项目有二种方法：一种是先克隆父项目，再更新子模块；另一种是直接递归克隆整个项目。

### 方法一：先克隆父项目，再更新子模块

#### ■ 克隆父项目

```sh
$ git clone https://github.com/cain/cain-assets.git test
```

#### ■ 查看子模块 

```sh
$ git submodule
 --e23e823d3f51f5ebd731a68da05ad0371c3a0231 test
```

子模块前面有一个--，说明子模块文件还未检入（空文件夹）。 

#### ■ 初始化子模块

```sh
$ git submodule init
Submodule 'test' (https://github.com/cain/cain-test.git) registered for path 'test'
```

####  ■ 更新子模块

```sh
$ git submodule update
Cloning into 'test'...
remote: Counting objects: 151, done.
remote: Compressing objects: 100% (80/80), done.
remote: Total 151 (delta 18), reused 0 (delta 0), pack-reused 70
Receiving objects: 100% (151/151), 1.34 MiB | 569.00 KiB/s, done.
Resolving deltas: 100% (36/36), done.
Checking connectivity... done.
Submodule path 'test': checked out 'e23e823d3f51f5ebd731a68da05ad0371c3a0231'
```


在更新的过程中，可能要求输入git的用户名和密码。

### 方法二：递归克隆整个项目 

```sh
$ git clone https://github.com/cain/cain-test.git test --recursive 
```


递归克隆整个项目，子模块已经同时更新了，比方法一简洁。 

## 七.删除子模块 

**删除子模块比较麻烦，需要手动删除相关的文件，否则在添加子模块时有可能出现错误。**

#### ■删除子模块文件夹

```sh
$ git rm --cached test
$ rm -rf test
```

#### ■删除.gitmodules文件夹中相关子模块信息 

```sh
[submodule "assets"]
  path = test
  url = https://github.com/cain/cain-test.git
```

#### ■删除.git/config文件夹中的相关子模块信息 

```sh
[submodule "test"]
  url = https://github.com/cain/cain-test.git
```

#### ■删除.git文件夹中的相关子模块文件 

```sh
$ rm -rf .git/modules/test
```

