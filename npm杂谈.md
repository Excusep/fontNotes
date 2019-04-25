### npm杂谈

#### npm install

* npm install modName  // 安装模块到项目目录下
* npm install -g modName  // -g 的意思是将模块安装到全局，具体安装到磁盘哪个位置，要看 npm config prefix 的位置。
* npm install -save moduleName  //  -save 的意思是将模块安装到项目目录下，并在package文件的dependencies节点写入依赖。
* npm install -save-dev moduleName  //  -save-dev 的意思是将模块安装到项目目录下，并在package文件的devDependencies节点写入依赖。

#####  -save 和 -save-dev的区别

* -save
  * 运行npm install --production或者注明NODE_ENV变量值为production时，**会**自动下载模块到node_modules目录中。
*  -save-dev
  * 运行npm install --production或者注明NODE_ENV变量值为production时，不会自动下载模块到node_modules目录中。