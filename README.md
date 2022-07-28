```
git clone https://github.com/ovolh/hugo-blog-doit.git --recursive

git submodule update --remote --merge
git submodule update --init --recursive    下拉子模块

更新 submodule

git submodule -q foreach git pull -q origin master
```

## 使用命令
1. 启动
```
hugo serve -e production -D --disableFastRender
```
2. 正式运行
```
hugo
```