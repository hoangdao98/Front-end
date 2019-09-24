# Animation
`animation` là một thuộc tính trong css, nó có thể sử dụng để tạo các hiệu ứng chuyển động mà không cần phải sử dụng đến javascript. Mỗi `animation` sẽ được đi kèm với `@keyframes`, để dễ hiểu hơn thì ta sẽ hình dung ra nó là như này.

```css
.element {
  animation: animationName 5s;
}

@keyframes animationName {
  0% {
    background-color: #001F3F;
  }
  100% {
    background-color: #FF4136;
  }
}
```
Trong tổng thời gian là 5s, ở `@keyframes` 0% (thời gian bắt đầu) thì màu của nó sẽ là `#001F3F`. Nó sẽ chạy đến `@keyframes` 100% (giây thứ 5) và background-color lúc này sẽ dần dần được chuyển sang màu `#FF4136`.

<p class="codepen" data-height="336" data-theme-id="dark" data-default-tab="css,result" data-user="hoangdao98" data-slug-hash="OJLrrgB" style="height: 336px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Animation">
  <span>See the Pen <a href="https://codepen.io/hoangdao98/pen/OJLrrgB">
  Animation</a> by hoangdao98 (<a href="https://codepen.io/hoangdao98">@hoangdao98</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

Ngoài ra animation css còn cho ta thêm 8 thuộc tính khác để tăng tính tùy biến. Như trong ví dụ trên, mình đang dùng 1 thuộc tính animation-iteration-count: infinite (chạy mãi mãi). Thế các thuộc tính còn lại là gì thì mình tìm hiểu ngay sau đây.

# Các thuộc tính trong animation.
* animation-name: Khai báo tên cho @keyframes.
* animation-duration: Thời gian mà bạn muốn cho một animation cycle.
* animation-timing-function: Xác định tốc độ chuyển động của một animation ví dụ như ease hoặc linear.
* animation-delay: Độ trễ của mỗi animation.
* animation-direction: Hướng di chuyển của animation.
* animation-iteration-count: Số lần animation được thực hiện.
* animation-fill-mode: Áp dụng css trước hoặc sau khi chạy animation.
* animation-play-state: pause/play animation.

## animation-duration
Cú pháp: 
```css
animation-duration: time;
```
`time` có thể là `s` hoặc `ms`

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="hoangdao98" data-slug-hash="xxKmBLv" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Animation duration">
  <span>See the Pen <a href="https://codepen.io/hoangdao98/pen/xxKmBLv">
  Animation duration</a> by hoangdao98 (<a href="https://codepen.io/hoangdao98">@hoangdao98</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
## animation-timing-function
Cú pháp:
```css
animation-timing-function: value;
```
Value sẽ bao gồm 1 trong các giá trị dưới đây:
* linear: Chuyển động cùng tốc độ từ đầu đến khi kết thúc.
* ease: Chuyển động ban đầu sẽ chậm, sau đó nhanh, kết thúc thì sẽ từ từ. Đây là dạng mặc định của animation.
* ease-in: Chuyển động ban đầu chậm sau đó sẽ nhanh dần.
* ease-out: Ngược lại với ease-in.
* ease-in-out: Chuyển động ban đầu chậm, sau đó nhanh, đến lúc kết thúc sẽ chậm dần.
* cubic-bezier(n, n, n, n): Xác định giá trị riêng cho chuyển động, giá trị sẽ từ 0 tới 1. (tu bi con tờ niu)

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="hoangdao98" data-slug-hash="pozqXwK" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Animation-timing-function">
  <span>See the Pen <a href="https://codepen.io/hoangdao98/pen/pozqXwK">
  Animation-timing-function</a> by hoangdao98 (<a href="https://codepen.io/hoangdao98">@hoangdao98</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## animation-delay
Cú pháp: 
```css
animation-delay: time;
```
<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="hoangdao98" data-slug-hash="pozGrGv" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="pozGrGv">
  <span>See the Pen <a href="https://codepen.io/hoangdao98/pen/pozGrGv">
  pozGrGv</a> by hoangdao98 (<a href="https://codepen.io/hoangdao98">@hoangdao98</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## animation-direction
Cú pháp:
```css
animation-direction: value;
```
Value sẽ bao gồm 1 trong các giá trị dưới đây:
* normal: amimation chạy bình thường.
* reverse: animation sẽ chạy ngược lại bình thường.
* alternate: chuyển động sẽ đảo ngược lại ngay sau khi kết thúc 1 chu kỳ.
* alternate-reverse: chuyển động sẽ đảo ngược trước, sau đó lại giống alternate.
## animation-iteration-count
Cú pháp:
```css
animation-iteration-count: value
```
Value sẽ bao gồm 1 trong các giá trị sau:
* Các số lớn hơn 0 (mặc định sẽ là 1)
* infinite: chạy vô hạn.

## animation-fill-mode
Cú pháp:
```css
animation-fill-mode: value;
```
Value sẽ bao gồm 1 trong các giá trị sau:
* none: Đây là giá trị mặc định. Khi kết thúc animation thì nó không thêm style nào trong animation vào DOM html.
* forwards: Khi kết thúc animation, nó sẽ apply hết các thuộc tính cuối cùng (thuộc tính ở @keyframes 100%) của animation vào DOM html.
* backwards: Khi kết thúc animation, nó sẽ apply hết các thuộc tính đầu tiến (thuộc tính ở @keyframes 0%) của animation vào DOM html.
* both: ... =)))
## animation-play-state
Cú pháp:
```css
animation-play-state: value;
```
Value sẽ là 1 trong các giá trị sau:
* paused: Tạm dừng chuyển động
* running: Tiếp tục chuyển động

## Rút gọn
Nếu bạn không muốn viết lại chi tiết các thuộc tính trên thì có thể viết gọn lại như sau:
Cú pháp:
```css
animation: [name] [duration] [timing] [delay] [interaction-count] [direction] [fill-mode] [play-state]
```

```css
@keyframes stretch {
  /* declare animation actions here */
}

.element {
  animation-name: stretch;
  animation-duration: 1.5s; 
  animation-timing-function: ease-out; 
  animation-delay: 0s;
  animation-direction: alternate;
  animation-iteration-count: infinite;
  animation-fill-mode: none;
  animation-play-state: running; 
}

/*
  Rút gọn nó sẽ thành như này.
*/

.element {
  animation: 
    stretch
    1.5s
    ease-out
    0s
    alternate
    infinite
    none
    running;
}
```

# Multiple steps
Nếu bạn muốn animation giống nhau khi bắt đầu và khi kết thúc,
Ta có dùng dấu phẩy để ngăn cách giữa các keyframe như này:
```css
@keyframes animationName {
  0%, 100% {
    background-color: yellow;
  }
  50% {
    background-color: red;
  }
}
```
# Multiple animation
Nếu muốn nhiều animation trong 1 lần thì sao? Nó cũng tương tự như multiple steps, ta cũng dùng dấu phẩy để ngăn cách giữa các animation.
```css
.element {
  animation: 
    pulse 3s ease infinite alternate, 
    nudge 5s linear infinite alternate;
}
```

# Ứng dụng animation vào thực tế.

<p class="codepen" data-height="265" data-theme-id="dark" data-default-tab="css,result" data-user="antho-fsy" data-slug-hash="wJqWKj" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="CSS Reveal animation text and image">
  <span>See the Pen <a href="https://codepen.io/antho-fsy/pen/wJqWKj">
  CSS Reveal animation text and image</a> by Anthony Fessy (<a href="https://codepen.io/antho-fsy">@antho-fsy</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

...
# Tổng kết
# Nguồn tham khảo.

<script async src="https://static.codepen.io/assets/embed/ei.js"></script>