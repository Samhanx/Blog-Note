# 利用npx来执行命令行工具.md

npx 是 npm 在 5.2 以上版本提供的一个包执行工具

过去如果要执行一个包的命令，要么通过全局安装将可执行文件注册到环境变量直接执行

要么将模块安装到本地，通过这样来执行

```bash
./node_modules/.bin/xxxxxx

# 或者
`npm bin`/xxxxxx

# 或者通过 run npm scripts 来执行
```

现在可以直接通过 `npx xxxxx` 执行

甚至可以不用安装这个包，来临时执行，对于只需要偶尔执行一次命令的包非常好用

```bash
# 基本语法
npx -p <packagename> -c 'cammand string'

# 一个示例
npx -p cowsay -p lolcatjs -c 'echo hello world' | cowsay | lolcatjs
```

比如 vue-cli 通常会全局安装来使用，利用 npx 就不用安装，会在执行时临时下载

```bash
npx -p vue-cli -c 'vue init webpack testvue'
```