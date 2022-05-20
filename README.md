# weiboPicDownloader (fork) ![](https://img.shields.io/badge/python-3.7+-blue.svg)

Forked from https://github.com/nondanee/weiboPicDownloader

Major improvements:
* Now can download posts with more than 9 pictures, also fixed some bugs
* Cleanup text from the weibo when used in name template
* Refactored as a module for easier incorporating into other Python scripts/projects. It now returns a list of dict to show some stats from the download session too.

Breaking changes:
* Dropped Python 2 support
* `-b` (boundary) now is NON-inclusive on the left-side (earlier date). This is done to make it easier to update (so you can use `-b last_checked_bid:` to only download new posts without overlapping). `-b` with s specific mid/bid (instead of a range) would still download that specific post.

Weibo user album batch download tool (CLI)

for more weibo free login APIs, turn to [wiki](https://github.com/nondanee/weiboPicDownloader/wiki)

~~**[中文 README](README-CN.md)**~~ (未更新)

## References

* [nondanee/weiboPicDownloader](https://github.com/nondanee/weiboPicDownloader) (original repo)
* [yAnXImIN/weiboPicDownloader](https://github.com/yAnXImIN/weiboPicDownloader)  
* [ningshu/weiboPicDownloader](https://github.com/ningshu/weiboPicDownloader) 

## Overview

![](https://user-images.githubusercontent.com/26399680/51592598-fd48b980-1f2a-11e9-9687-4670e7dfcd83.png)

## Dependencies

```
$ pip install requests
$ pip install colorama # only windows version under 10.0.14393 required
```

## Usage

```
$ python .\weiboPicDownloader.py -h
usage: weiboPicDownloader [-h] (-u user [user ...] | -f file [file ...])
                          [-d directory] [-s size] [-r retry] [-i interval]
                          [-c cookie] [-b boundary] [-n name] [-v] [-o]

optional arguments:
  -h, --help          show this help message and exit
  -u user [user ...]  specify nickname or id of weibo users
  -f file [file ...]  import list of users from files
  -d directory        set picture saving path
  -s size             set size of thread pool
  -r retry            set maximum number of retries
  -i interval         set interval for feed requests
  -c cookie           set cookie if needed
  -b boundary         focus on weibos in the id range
  -n name             customize naming format
  -v                  download videos together
  -o                  overwrite existing files
```

Required argument (choose one)

- `-u user ...` users (nickname or id)
- `-f file ...` user list files (nickname or id, separated by linefeed in the file)

Optional arguments

- `-d directory` media saving path (default value: `./weiboPic`)
- `-s size` thread pool size (default value: `20`)
- `-r retry` max retries (default value: `2`)
- `-i interval` request interval (default value: `1`, unit: second)
- `-c cookie` login credential (only need the value of a certain key named `SUB`)
- `-b boundary` mid/bid/date range of weibos (format: `id:id` between, `:id` before, `id:` after, `id` certain, `:` all). Use `@%Y%m%d` (like `@20220520` for date; otherwise integers would be considered as mid.)
- `-n name` naming template (identifier: `url`, `index`, `type`, `mid`, `bid`, `date`, `text`, `name`, `uid`,  like ["f-Strings"](https://www.python.org/dev/peps/pep-0498/#abstract) syntax)
- `-v` download miaopai videos at the same time
- `-o` overwrite existing files (skipping if exists for default)

*✳How to get the value of `SUB` from browser (Chrome for example)

1. Go to https://m.weibo.cn and log in
2. Inspect > Application > Cookies > https://m.weibo.cn
3. Double click the `SUB` line and copy its value
4. Paste it into terminal and run like  `-c <value>`
