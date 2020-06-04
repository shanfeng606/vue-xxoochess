## 知识点
### 创建
安装`vue-cli`脚手架工具
`$ vue create .  ` 在当前目录下创建项目
`$ yarn serve  ` 运行当前项目


### 主要文件
`App.vue`主要写代码的
`main.js` 启动文件，将`App.vue`渲染到` HTML`中的` #app `上去

### 组件化
重复的代码提取到组件中
在`App.vue`通过`import Cell from "./Cell"`引入

### 父子组件传值
父组件通过v-bind讲n传给子组件如下：
```html
<Cell @click="onClickCell" :n="n"/>
```
子组件通过prop接受
```javascript
export default {
  props: ["n"]
}
```
同理，通过con参数，判断棋盘是否可以继续下棋

### $emit
子组件可以通过`$emit`触发父组件的自定义事件。
```javascript
this.$emit("click", this.text);  //将text传给父组件
```
<img src='' width=400></img>


### 胜负判定机理
设置一个map记录每个格子的状态
```javascript
data() {
    return {
      n: 0,
      map: [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ],
    };
  }
```
每次点击事件给每个格子赋值，从而进行判断
```javascript
this.map[Math.floor(i / 3)][i % 3] = text;
      this.n = this.n + 1;
      this.tell();
```



### setTimeout
使用alert会发生堵塞，result不更新，利用setTimeout可避免阻塞
```javascript
if (this.result !== "胜负未分" && this.result !== null) {
        setTimeout(function() {
          alert(`游戏结束，胜方为${temp.result}`,);
        }, 100);
      }else if(this.n === 8 && this.result !== "胜负未分") {
        setTimeout(function() {
          alert("未分出胜负");
        }, 100);
      }
```
注意，这里setTimeout又是一个函数，此需设置`var temp = this;`拿到外面的this



### 浏览器刷新
用来重置棋局
```javascript
reset() {
      location.reload();
    }
```
