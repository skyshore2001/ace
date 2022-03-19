# 开发说明

ace使用requirejs模块机制，免编译即可运行，比如直接用apache打开示例：

	http://localhost/d/src/ace/kitchen-sink.html

分支jdcloud: 为筋斗云addon开发定制的版本，主要用到js和php。

## 打包

	npm i
	make build

注意在打包后，所有css及图片也是自动打到js中去的。

一般外部建议使用 build/src-min-noconflict 版本，其中require/define被改名为ace.require/ace.define.

为jdcloud定制的版本，使用jdcloud分支。
在jdcloud项目的`server/web/lib/`目录下配置并执行`_copy_ace.sh`，可将文件复制到`server/web/lib/ace`目录下。

## 修改记录

### 自动提示功能

自动提示需要引入文件`ace/ext-language_tools.js`。

设置选项：

	enableBasicAutocompletion: true,
	enableSnippets: true,
	enableLiveAutocompletion: true, // 如果为false, 则仅当按快捷键时才提示

如果未开启enableLiveAutocompletion，则需要通过快捷键激活提示，缺省快捷键是

    bindKey: "Ctrl-Space|Ctrl-Shift-Space|Alt-Space"

由于快捷键冲突，源码中已改为"Alt-/"；

其实也可以调用前配置，如：

	ace.require("./autocomplete").Autocomplete.startCommand.bindKey = "Ctrl-Space|Ctrl-Shift-Space|Alt-/"

### javascript默认使用最新es10

2022/03/20

JS中使用async/await会报警说要用`esversion: 8`：

	async function f() {}

代码前加注释`/* jslint esnext: false, esversion: 8 */` 可以解决。
此处还是更新为es10兼容性更好。

