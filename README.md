# Virtual-scrolling-of-long-list

## 1.设置列表容器的样式

```css
<style>
    .container {
      position: relative;
      width:1000px;
      max-height: 900px; /* 设置容器视图区域的大小 */
      margin: 0;
      padding: 0;
      border: 1px solid #000;
      overflow-y: auto;
      list-style-type: none;
    }
    .container li {
      position: absolute;
      width: 100%;
      height: 50px;
      color: yellow;
      text-align: center;
      line-height: 40px;
    }
</style>
```

## 2.生成数据并渲染成5000个列表项li 高度设置为45px

```js
<script>
	const data_list = Array.from({ length: 5000 }).map((item, index) => index); // 生成五千条数据
	const list = document.querySelector(".container");
	list.setAttribute("style", `height: ${45 * dataList.length}px;`); // 设置列表的总高度
</script>
```

### 3.创建li函数

```js
function create_li(index) {
      	// list 容器， size为展示li数量， index为第一条数据的索引值
        list.innerHTML = dataList.slice(index, index + size).map(
          item =>
            `<li style="top: ${item * 50}px; background: ${createHexColor()};">${item}</li>`)
          .join("");
      }
```

## 4.监听滚动确定index值

```js
根据列表的滚动距离（scrollTop）除以列表项（item）的大小，可以确定第一条数据的索引值i
list.onscroll = handleScroll;
      function handleScroll(e) {
        const index = Math.floor(e.target.scrollTop / 50);
        create_li(index);
      }
```

## 5.监听滚动函数进行节流优化

```js
function throttle(fn, delay) {
          let lastTime = 0;
          return function (...arg) {
            const currentTime = +new Date();
            if (currentTime - lastTime > delay) {
              fn.apply(this, arg);
              lastTime = currentTime;
            }
          };
        }
```

