# Webgpu

- 安裝 Node.js
https://nodejs.org/zh-tw/download/

- 建立專案資料夾(此處以 project 1 為例)
mkdir project\ 1

- 進入專案資料夾
cd project\ 1/

- 初始化，產生 package.json  (-y 代表所有選項使用預設)
npm init -y

- 安裝 jquery
npm i jquery

- 安裝 @types/jquery
npm i @types/jquery

- 安裝 style-loader css-loader ts-loader
npm i style-loader css-loader ts-loader

- 安裝 typescript
npm i typescript

-對 package.json 中的 scripts 進行修改
```javascript
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```
改成以下
```javascript
  "scripts": {
    "dev": "webpack --mode development",
    "prod": "webpack --mode production",
    "watch": "webpack --watch --mode production"
  },
```