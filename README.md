细刻doc
==========


1.Mac工具安装
-----------

使用Mac需要安装应用的命令

> **Note**
> - Xcode: 在APP Store即可下载
> - Homebrew: 是Mac OSX上的软件包管理工具，能在Mac中方便的安装软件或者卸载软件
> - Homebrew Install:
```sh
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
> - 查看安装应用，包括版本号: 
```sh
$ brew list --versions
```
> - Homebrew Cask(Homebrew扩展): 
```sh
$ brew install caskroom/cask/brew-cask
```
> - Homebrew 安装应用demo: 
```sh
$ brew cask install google-chrome
```
> - Tip: Homebrew Cask网页链接 <i class="icon-upload"></i> http://sourabhbajaj.com/mac-setup/Homebrew/Cask.html.


2.本地服务环境配置
------------------

> **Note**
> **在启动你的 Homestead 环境之前，你必须先安装 VirtualBox 和 Vagrant.**
> - virtualbox install: 
```sh
$ brew install Caskroom/cask/virtualbox
```
> - Vagrant install: 
```sh
$ brew install Caskroom/cask/vagrant
```
> - Homestead配置(laravel链接说明): http://laravel-china.org/docs/5.0/homestead
> - Tips:从github上clone下来的Homestead配置文件，恢复到`2277085`版本号，然后用vbox的0.3.3版本，这个都已经提前下载好了，最新版的不能支持本地安装，从本地安装的命令是：`vagrant box add laravel/homestead /path/to/local/0.3.3.vbox`
	

3.代码部署配置
--------------

> **Note**
> **获取代码之前先安装git应用**
> - git install: 
```sh
$ brew install Caskroom/cask/git
```
> - git的一些使用方法: http://git-scm.com/docs/gittutorial
> - git的提交原理: https://git-scm.com/book/en/v2/Getting-Started-Git-Basics


4.webpack 配置教程
--------------




```
var webpack = require('webpack');
//ExtractTextPlugin插件是非常实用的一个插件，webpack的默认行为会把js里引入的css代码注入到行内，这样就无法使用缓存了，此插件就是可以把css代码，或者是其他的一些字节流输出到一个文件
var ExtractTextPlugin = require("extract-text-webpack-plugin");

module.exports = {
//是一个入口文件，可以配置成多个
	entry: {
		'main' : './js/main'
		,'main2' : './js/main2'
	},
	//输出的文件名称是根据entry里的key生成的，chunkFilename这个参数没搞懂有什么意义，path规定了所有输出的文件的根目录，publicPath定义了css代码中url的前缀，非常重要的一个参数
	output: {
		filename: './js/[name].bundle.js',
		chunkFilename: "[id].js",
		path : './dist',
		publicPath : '../'
	},
	//模块加载器
	module : {
		loaders : [
			//加载style和css两个loader，并且以文件的形式输出到 output 配置的相对应的路径中去
			{ test: /\.css$/, loader: ExtractTextPlugin.extract("style-loader", "css-loader")},
			//加载url loader，参数的意义是：limit小于此数值的图片可以直接转换为base64的图片，name的意义是[path]对应实际的文件夹路径,[name]对应着文件名,[ext]对应着文件扩展名,[hash]随机数，清除缓存用的，有多种方式生成，默认是md5
			{test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192&name=[path][name].[ext]?[hash]'},
			//预编译sass文件，继续配合使用ExtractTextPlugin插件，可以将编译后的css代码提取出来并输出到.css文件中去。so，加载的时候，不管是css还是sass或者是less都会编译好，输出到.css中去，超级方便。
			{ test: /\.scss$/, loader: ExtractTextPlugin.extract("style", "css!sass")},
			//匹配字体库，并且移动到output配置中相对应的文件夹中去，这里用的是file-loader，url-loader这两个loader大同小异，url-loader是对file-loader的二次封装，我猜测目的是为了支持limit，可以将有写图片转换为base64
			{test: /\.(ttf|eot|svg|woff(2)?)(\?[a-z0-9]+)?$/,loader : 'file-loader?name=[path][name].[ext]?[hash]'}
		]
	},
	//插件配置项
	plugins: [
		//超级赞的优化插件，第一个参数固定，不知道支持的其它参数有什么意义，用到再看文档吧。当在所有资源中引入次数>=2次，就会被提取出来，并且压入到vendor.js中去的
		new webpack.optimize.CommonsChunkPlugin("commons", "vendor.js",2),
		//生成相对应的css代码，[name]对应着entry中的key
		new ExtractTextPlugin("./css/[name].css",{
			allChunks: true
		}),
		//全局化一些变量，使用webpack之后，基本上消灭了全局变量，但我们有时候不得不暴露出一些全局变量来，这个插件就是暴露全局变量的
		new webpack.ProvidePlugin({
			$: "jquery",
			jQuery: "jquery",
			"window.jQuery": "jquery"
		})
		//压缩混淆代码的插件，可以不用这个插件，在命令中-p，能起到同样的效果，在这里属于鸡肋。
		,new webpack.optimize.UglifyJsPlugin({
			compress: {
				warnings: false
			}
		})

	]
};
```

```
//Tool.js
var Tool = (function(){
    return {
        'test' : function(){
            console.log('this is from tool.js')
        }
    }
}());
module.exports = Tool;
```
```
//main.js
var tool = require('./tool');
require('../css/base.css');
require('../css/home.css');
require('../css/category.css');
require('../css/font/css/font.css');
require('../css/base.scss');
$('body').append('this is main');
```
```
//main2.js

var tool = require('./tool');
require('../css/base.css');
require('../css/home.css');
require('../css/base.scss');
$('body').append('<br/>hello this is main2');
console.log(tool)
```

