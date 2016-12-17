#
Update CSS Variables with JS

demo:
https://telsaiori.github.io/Update-CSS-Variables-with-JS/index.html

javascript30:
https://javascript30.com


先在root裡面命名變數,變數開頭一定要是"--",且會分辨大小寫為不同變數
```
:root {
--base: #ffc600;
--spacing: 10px;
--blur: 10px;
}
```
要使用時像下面這樣,就會按照變數去設定了
```
img {
padding: var(--spacing);
background: : var(--base);
filter: var(--blur);
}
```
http://codepen.io/mukiwu/pen/PNZzbd

也可以在其他selector裡面定義變數,讓不同的地方套用不一樣的顏色

接下來需要抓三個input的value
```
function handleUpdate(){
console.log(this.value);
}

inputs.forEach(input => input.addEventListener('change', handleUpdate));
```

像上面那樣雖然可以順利抓到值,但要在滑鼠放開的時候才會觸發,滑鼠移動的時候不會有功用,所以要再加入偵測滑鼠移動event
```
inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));
```
但因為spacing和blur的設定是數字+px,照上面的寫法只抓得到數字,沒辦法直接拿來用,所以這個案例在input後面加了data來定義他們的單位
```
<input type="range" name="spacing" min="10" max="200" value="10" data-sizing="px">

<label for="blur">Blur:</label>
<input type="range" name="blur" min="0" max="25" value="10" data-sizing="px">
```
我們可以使用**dataset**來抓取所有的data內容
```
const suffix = this.dataset;
```
最後完成的function如下
```
function handleUpdate(){
// console.log(this.value);
const suffix = this.dataset.sizing || '';
document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
}
```
suffix是用來抓data的值,因為base沒有設定data,所以多了or去判斷



