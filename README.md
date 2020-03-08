# FE-note

## 浏览器渲染机制

+ 浏览器解析`html`文件
+ 根据`html`，从上到下，构建`DOM`树
+ 遇到`css`样式，构建`CSSOM`
   + 外链`CSS`：加载`CSS`文件，不阻塞`DOM`的构建
   + 阻塞`render`树的构建
+ 遇到`js`文件
   + 外链`js`文件：
      + `<script src="/*"></script>`，加载`js`文件，渲染此`js`之前的dom到页面上，阻塞之后的`DOM`构建，加载完成后，立即执行`js`文件，执行完成后从当前位置继续解析DOM
      + `<script src="/*" async></script>`，有`async`的属性，加载js文件，并不会阻塞`DOM`的构建，`js`加载完毕后，立即执行`js`脚本
      + `<script src="/*" defer></script>`，有`defer`的属性，加载js文件，并不会阻塞`DOM`的构建，`js`加载完毕后，等到`DOM`解析完成后，在`DOMContentLoaded`之前，执行js脚本
+ `DOM`树与`CSS`树，生成`render`树
   + `render`树的生成，在第一次加载页面的时候，可能不止一次，它会在合适的时机生成，并渲染到浏览器上。--- 比如说，第一次遇到`js外链文件`时
   + `render`树，包含了每个节点的样式
+ 浏览器根据render树，获取每个节点的几何信息（位置、大小），这一阶段，为`reflow`（`回流`）
+ `reflow`之后，会计算出，对于当前浏览器的实际像素值，并发送给浏览器，进行显示，这一阶段，为layout（`重绘`）
