## 包含webpack 1和webpack2 的版本特性.

### webpack.config.js文件:
```

const webpack = require('webpack')
module.exports = {
    entry: './src/js/app.js',
    output: {//输出resolve
        path: __dirname+'/src/dist', //输出路径,绝对路径

        // path: path.resolve(__dirname,'src'),
        filename: 'bundle.js'//输出到dist的文件名称:bundle.js
    },
    module: {//模块
        rules: [{
            test: /\.js?$/,//以.js结尾就交给loader处理
            exclude: /node_modules/,//排除这个目录的文件,我们排除node_modules这里，因为否则所有外部lib也将通过babel，减慢编译速度。
            loader: 'babel-loader',//什么作用:转成浏览器目前可识别的代码,jsonloader转成浏览器识别的json,合种xxxloader作用都是转浏览器识别的格式
            //Loader 可以理解为是模块和资源的转换器，它本身是一个函数，接受源文件作为参数，返回转换的结果。这样，我们就可以通过 require 来加载任何类型的模块或文件，比如 CoffeeScript、 JSX、 LESS 或图片
        }]

    },
    plugins: [//插件  optimize:优化
        new webpack.optimize.UglifyJsPlugin({//您需要在工作流程中对捆绑包进行一些额外的处理。一个例子是将您的文件缩小，以便客户端可以更快地加载它。这可以用插件完成。我们将添加uglify插件到我们的配置： 
            compress: {
                warnings: false,
            },
            output: {
                comments: false,
            },
        }),
    ]
}

//运行逻辑,
//网页打开html文件,加载bundle.js文件.这个加载bundle.js文件实际是已经打包好部分资源的包文件.本质是按需加载,所以首屏打开的时间不会太长.测试下时间
//主要说下webpack打包的逻辑
//在webpack.config配置文件信息
//entry进入哪里的文件
//output输出到哪里.
//module rules :转换浏览器认识的格式,遇到什么不识别的文件就用对应的loader转换.如转换es6语法,sass的文件..
//plugins :性能的优化,如压缩图片,压缩文件...

```

## package.json

```
{
  "name": "s5-webpack",
  "version": "1.0.0",
  "description": "",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start":"webpack"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "webpack": "^2.6.1"
  }
}

```

## app.js:entry文件
```
//webpack方式
//为什么有main.js这文件
var $ = require('../lib/jquery-3.2.1.min.js')
var Carousel = require('./carousel.js')
var GoTop = require('./gotop.js')
var AddMore = require('./addmore.js')


Carousel.init($('.carousel'))
GoTop.init()
AddMore.init($('.btnMore'))
```
