# 判断js是否进行混淆或压缩

## 原理

使用js的压缩器(minifiers)或混淆器进行代码转换（webpack打包的时候可以加这些工具）, 为了使生成的代码具有更小的体积，会删除多余的空格与换行符，并且将函数名
变量名进行替换成简单简短的名称。

## 方法

利用函数名、变量名改变的这一特点，通过函数名称是否改变进行判断js是否进行混淆或压缩。

```
function isMiniFy () {
  if (
    typeof isMiniFy.name === 'string'
    && isMiniFy.name !== 'isMiniFy'
  ) {
    console.log('代码已被混淆！');
  }
}

```
1. 定义了一个isMiniFy的函数，函数内部判断了isMiniFy的name属性是否存在，并且是否为string类型。
2. 判断isMiniFy的name属性是否等于isMiniFy，如果相等，说明isMiniFy没有更改名称，即没有被混淆或压缩。

## 应用

在redux js的源码index.js文件中，进行了这样的判断。
```
/*
 * This is a dummy function to check if the function name has been altered by minification.
 * If the function has been minified and NODE_ENV !== 'production', warn the user.
 */
function isCrushed() {}

if (
  process.env.NODE_ENV !== 'production' &&
  typeof isCrushed.name === 'string' &&
  isCrushed.name !== 'isCrushed'
) {
  warning(
    'You are currently using minified code outside of NODE_ENV === "production". ' +
      'This means that you are running a slower development build of Redux. ' +
      'You can use loose-envify (https://github.com/zertosh/loose-envify) for browserify ' +
      'or setting mode to production in webpack (https://webpack.js.org/concepts/mode/) ' +
      'to ensure you have the correct code for your production build.'
  )
}
```

