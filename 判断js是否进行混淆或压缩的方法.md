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
