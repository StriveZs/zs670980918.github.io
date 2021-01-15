---
title: Anaconda Clean命令

categories:
  - MAC
  - Anaconda

tags:
  - Anaconda
  - Clean
---

# Anaconda Clean命令
conda 安装的包都在目录Anaconda/pkgs下。随着使用，conda 安装的包也越来越多；有时候会出现以下不好的情况：

有些包安装之后，从来没有使用过；
一些安装包的tar包也保留在了计算机中；
由于依赖或者环境等原因，某些包的不同版本重复安装。
上面的这些情况使得anaconda显得更加冗余，并且浪费储存；对于这些情况可以使用conda clean 净化Anaconda。

## 查看conda clean使用参数
```
$ conda clean -H
usage: conda clean [-h] [-a] [-i] [-l] [-p] [-t] [-f]
                   [-c TEMPFILES [TEMPFILES ...]] [-d] [--json] [-q] [-v] [-y]

Remove unused packages and caches.

Options:

optional arguments:
  -h, --help            Show this help message and exit.

Removal Targets:
  -a, --all             Remove index cache, lock files, unused cache packages,
                        and tarballs.
  -i, --index-cache     Remove index cache.
  -l, --lock            Remove all conda lock files.
  -p, --packages        Remove unused packages from writable package caches.
                        WARNING: This does not check for packages installed
                        using symlinks back to the package cache.
  -t, --tarballs        Remove cached package tarballs.
  -f, --force-pkgs-dirs
                        Remove *all* writable package caches. This option is
                        not included with the --all flag. WARNING: This will
                        break environments with packages installed using
                        symlinks back to the package cache.
  -c TEMPFILES [TEMPFILES ...], --tempfiles TEMPFILES [TEMPFILES ...]
                        Remove temporary files that could not be deleted
                        earlier due to being in-use. Argument is path(s) to
                        prefix(es) where files should be found and removed.

Output, Prompt, and Flow Control Options:
  -d, --dry-run         Only display what would have been done.
  --json                Report all output as json. Suitable for using conda
                        programmatically.
  -q, --quiet           Do not display progress bar.
  -v, --verbose         Can be used multiple times. Once for INFO, twice for
                        DEBUG, three times for TRACE.
  -y, --yes             Do not ask for confirmation.

Examples:

    conda clean --tarballs

```

## Conda clean使用
## 删除从不使用的包
```
$ conda clean --packages
```

## 删除tar包
```
$ conda clean --tarballs
```

##  删除索引缓存、锁定文件、未使用过的包和tar包
```
$ conda clean -a 
```

## 清楚索引缓存
```
$ conda clean -i
```

## 应用情况
今天我在使用conda安装opencv的时候一直报unexpected error的错误，经过一番尝试发现使用

```
conda clean -i
```

可以很好地解决该问题。