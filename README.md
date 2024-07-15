# 如何运行源代码

1. **安装依赖**
   
   在项目根目录下运行以下命令安装所有依赖：
   ```bash
   npm install

2. **启动开发环境**

    ```bash
    npm run serve


### 编译并压缩文件用于生产环境
运行以下命令将项目编译并打包成静态文件：（该命令会在项目根目录下生成一个 dist 目录，里面包含了打包后的静态文件。）
```
npm run build
```

### 检查并修复文件中的错误
```
npm run lint
```
<br><br>

# 如何运行可执行程序

## 前提条件

在运行打包后的可执行文件之前，请确保已经完成以下步骤：

1. **安装 Node.js 和 npm**
   确保系统上已经安装了 Node.js 和 npm。可以通过以下命令检查安装情况：
   ```bash
   node -v
   npm -v

## 使用 HTTP 服务器运行打包后的文件

1. **安装 serve**

    ```bash
    npm install -g serve

2. **运行 dist**

    在项目根目录下运行以下命令：
    ```bash
    serve -s dist
