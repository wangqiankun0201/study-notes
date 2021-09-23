# webpack打包

`npm init -y`   生成package.josn文件



在package.json文件中加入`"buile: 'webpack'"`



`cnpm i -D webpack webpack-cli typescript ts-loader`     依赖





==编写webpack配置文件==

webpack.config.js

```js
//引入一个块，作用是帮我们拼接路径
const path = require('path');
//webpack中的所有配置信息都应该写在module.exports中
module.exports = {
   //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output: {
        //指定打包文件的目录
        path: path.resolve(__dirname,'dist'),
        //打包后文件的名字
        filename: "bundle.js"
    },
    //指定webpack打包时打包时要是用的模块
    module: {
        //指定加载规则
        rules: {
            //指定规则生效的文件
            test:/\.ts$/,
            //指定要使用的loader
            use: "ts-loader",
            //要排出的文件
            exclude: /node-modules/            
        }
    }
}
```







==指定ts配置文件==

tsconfig.json



```json
{
    compilerOptions: {
        "module": "ES2015",
        "target": "ES2015",
        "strict": true
    }
}
```







`npm run bulid`   打包





`cnpm i -D html-webpack-plugin`  帮助我们自动生成html文件

配置webpack.config.js

```js
//引入一个块，作用是帮我们拼接路径
const path = require('path');
//引入html插件
const HTMLWebpackPlugin = require('html-webpack-plugin');
//webpack中的所有配置信息都应该写在module.exports中
module.exports = {
   //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output: {
        //指定打包文件的目录
        path: path.resolve(__dirname,'dist'),
        //打包后文件的名字
        filename: "bundle.js"
    },
    //指定webpack打包时打包时要是用的模块
    module: {
        //指定加载规则
        rules: {
            //指定规则生效的文件
            test:/\.ts$/,
            //指定要使用的loader
            use: "ts-loader",
            //要排出的文件
            exclude: /node-modules/            
        }
    },
    //配置webpack插件
    plugins: {
        new HTMLWebpackPlugin({
        //title: "这是一个自定义的title"
        template: "./scr/index.html"  //指定模板
    }),
    }
}
```







`cnpm i -D webpack-dev-server`    内置服务器

配置package.json

"start": "webpack serve --open chrome.exe"



`cnpm i -D clean-webpack-plugin`    清除dist目录

配置webpack.config.js

```js
//引入一个块，作用是帮我们拼接路径
const path = require('path');
//引入html插件
const HTMLWebpackPlugin = require('html-webpack-plugin');
//引入clean插件
const {CleanWebpackPlugin} = require("clean-webpack-plugin");
//webpack中的所有配置信息都应该写在module.exports中
module.exports = {
   //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output: {
        //指定打包文件的目录
        path: path.resolve(__dirname,'dist'),
        //打包后文件的名字
        filename: "bundle.js"
    },
    //指定webpack打包时打包时要是用的模块
    module: {
        //指定加载规则
        rules: {
            //指定规则生效的文件
            test:/\.ts$/,
            //指定要使用的loader
            use: "ts-loader",
            //要排出的文件
            exclude: /node-modules/            
        }
    },
    //配置webpack插件
    plugins: {
        new HTMLWebpackPlugin({
        //title: "这是一个自定义的title"
        template: "./scr/index.html"  //指定模板
    }),
    	new CleanWebpackPulgin()
    }
}
```







==设置引用模块==

```js
//引入一个块，作用是帮我们拼接路径
const path = require('path');
//引入html插件
const HTMLWebpackPlugin = require('html-webpack-plugin');
//引入clean插件
const {CleanWebpackPlugin} = require("clean-webpack-plugin");
//webpack中的所有配置信息都应该写在module.exports中
module.exports = {
   //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output: {
        //指定打包文件的目录
        path: path.resolve(__dirname,'dist'),
        //打包后文件的名字
        filename: "bundle.js"
    },
    //指定webpack打包时打包时要是用的模块
    module: {
        //指定加载规则
        rules: {
            //指定规则生效的文件
            test:/\.ts$/,
            //指定要使用的loader
            use: "ts-loader",
            //要排出的文件
            exclude: /node-modules/            
        }
    },
    //配置webpack插件
    plugins: {
        new HTMLWebpackPlugin({
        //title: "这是一个自定义的title"
        template: "./scr/index.html"  //指定模板
    }),
    	new CleanWebpackPulgin()
    },
    //设置引用模块
    resolve: {
        extensions: ['.ts', '.js']   //扩展名
    }
}
```





## babel

`cnpm i -D @babel/core @babel/preset-env babel-loader core-js`



==修改webpack.config.js== module

```js
//引入一个块，作用是帮我们拼接路径
const path = require('path');
//引入html插件
const HTMLWebpackPlugin = require('html-webpack-plugin');
//引入clean插件
const {CleanWebpackPlugin} = require("clean-webpack-plugin");
//webpack中的所有配置信息都应该写在module.exports中
module.exports = {
   //指定入口文件
    entry:"./src/index.ts",
    //指定打包文件所在目录
    output: {
        //指定打包文件的目录
        path: path.resolve(__dirname,'dist'),
        //打包后文件的名字
        filename: "bundle.js"
        //告诉webpack不使用箭头函数
        environment: {
        	arrowFunction: false
    	}
    },
    //指定webpack打包时打包时要是用的模块
    module: {
        //指定加载规则
        rules: {
            //指定规则生效的文件
            test:/\.ts$/,
            //指定要使用的loader
            use: [
                //配置babel
                {
                 	//指定加载器
                    loader: "babel-loder",
                    //设置babel
                    options: {
                        //设置预定义的环境
                        presets: [
                            [
                                //指定环境插件
                                "@bable/preset-env",
                                //配置信息
                                {
                                  //要兼容的目标浏览器
                                    targets: {
                                        "chorme":"88"
                                    },
                                    //指定corejs的版本
                                    "corejs":"3",
                                    //使用corejs的方式
                              "useBuiltIns"："usage"
                                }
                            ]
                        ]
                    }
                },
                'ts-loader'
            ],
            //要排出的文件
            exclude: /node-modules/            
        }
    },
    //配置webpack插件
    plugins: {
        new HTMLWebpackPlugin({
        //title: "这是一个自定义的title"
        template: "./scr/index.html"  //指定模板
    }),
    	new CleanWebpackPulgin()
    },
    //设置引用模块
    resolve: {
        extensions: ['.ts', '.js']   //扩展名
    }
}
```

