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
npm i typescript -g

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

-產生 tsconfig.json 
tsc --init


-將 tsconfig.json 裡的內容刪光，改成以下
```
{
    "compilerOptions": {
      "rootDir": "src",
      "outDir": "dist",
      "target": "es6",
      "lib": [
        "es2017",
        "dom"
      ],
      "types": [
        "node",
        "@webgpu/types"
      ],
      "module": "es2015",
      "esModuleInterop": true,
      "strict": true,
      "sourceMap": true
    },
    "exclude": [
      "node_modules"
    ]
  }
```

- 建立 src 資料夾
mkdir src

- 建立 dist 資料夾
mkdir dist

- 在 dist 裡新增 index.html ，並加入以下內容
```
<!DOCTYPE html>
<head>
   <meta charset="utf-8">
   <meta http-equiv="X-UA-Compatible" content="IE=edge">
   <title>WebGPU Step-by-Step 1</title>
   <meta name="description" content="">
   <meta name="viewport" content="width=device-width, initial-scale=1">
</head>

<body>
    <h1>Check whether your browser support WebGPU or not:</h1>
   <h2 id="id-gpu-check"></h2>
   <script src="main.bundle.js"></script>
</body>
</html>
```

- 安裝  @webgpu/types@0.1.12
npm i @webgpu/types@0.1.12

- 安裝  @types/node
npm i @types/node



- 在 src 中新建 helper.ts，並加入以下內容
```
export const CheckWebGPU = () => {
    let result = 'Great, your current browser supports WebGPU!';
    if (!navigator.gpu) {
        result = `Your current browser does not support WebGPU! Make sure you are on a system 
                    with WebGPU enabled. Currently, WebGPU is supported in  
                    <a href="https://www.google.com/chrome/canary/">Chrome canary</a>
                    with the flag "enable-unsafe-webgpu" enabled. See the 
                    <a href="https://github.com/gpuweb/gpuweb/wiki/Implementation-Status"> 
                    Implementation Status</a> page for more details.   
                    You can also use your regular Chrome to try a pre-release version of WebGPU via
                    <a href="https://developer.chrome.com/origintrials/#/view_trial/118219490218475521">Origin Trial</a>.                
                `;
    } 

    const canvas = document.getElementById('canvas-webgpu') as HTMLCanvasElement;
    if(canvas){
        const div = document.getElementsByClassName('item2')[0] as HTMLDivElement;
        canvas.width  = div.offsetWidth;
        canvas.height = div.offsetHeight;

        function windowResize() {
            canvas.width  = div.offsetWidth;
            canvas.height = div.offsetHeight;
        };
        window.addEventListener('resize', windowResize);
    }
    return result;
}
```

- 在 src 中新建 main.ts，並加入以下內容
```
import $ from 'jquery';
import { CheckWebGPU } from './helper';

$('#id-gpu-check').html(CheckWebGPU());
```

- 新建 webpack.config.js，並加入以下內容
```
const path = require("path");
const bundleOutputDir = "./dist";

module.exports = {
    entry: {
        main: "./src/main"  
    },
    output: {
        filename: "[name].bundle.js",
        path: path.join(__dirname, bundleOutputDir),
        publicPath: 'public/dist/'
    },
    devtool: "source-map",
    resolve: {
        extensions: ['.js', '.ts']
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: ['/node_modules/']
            },            
            { test: /\.tsx?$/, loader: "ts-loader" },        
            {
                test: /\.css$/i,
                use: ["style-loader", "css-loader"]
            }
        ]
    }
};
```

- 編譯 typescript
npm run prod

- 安裝 vs code 的 Live Server 插件

- 安裝 Chrome Canary

- 在 Chrome Canary 的網址列輸入 chrome:flags

- 搜尋 webgpu

- 設為 enable

- 在 index.html 中按右鍵，選擇 Open with live server

- 首次執行將瀏覽器設為 Chrome Canary

- 出現成功畫面，結束