## 安装
- A: 安装 Node.js
    - [官网下载](https://nodejs.org/en/)
- B: 利用 Node Version Manager
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```

## 查看版本号
```
npm -v 
```

## 初始化项目
```
npm init
```

### 添加依赖包
```
npm install [package]
npm install [package] --save
npm install [package] --dev
```

### 更新依赖包
```
npm install [package]@[version]
```

## 删除依赖包
```
npm uninstall [package]
npm uninstall [package] --save
```

## 安装所有的依赖包
```
npm i
```
or
```
npm install
```
