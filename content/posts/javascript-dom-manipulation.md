
---
title: "JavaScript: DOM Manipulation — Hướng dẫn chi tiết"
date: 2025-10-24
tags: ["javascript", "dom", "cơ bản"]
categories: ["javascript"]
---

## Giới thiệu

DOM (Document Object Model) là giao diện lập trình cho phép truy cập và thao tác cấu trúc một tài liệu HTML hoặc XML dưới dạng cây (tree) gồm các nút (nodes). DOM Manipulation nghĩa là thay đổi nội dung, cấu trúc hoặc kiểu trình bày của trang bằng JavaScript. Bài viết này hướng dẫn chi tiết từ khái niệm cơ bản đến các ví dụ thực tiễn, lỗi thường gặp và bài tập để bạn thực hành.

## Yêu cầu trước khi bắt đầu

1. Trình duyệt hiện đại (Chrome, Firefox, Edge) hoặc Node.js với môi trường DOM (ví dụ JSDOM) nếu cần test ngoài trình duyệt.
2. Một trình soạn thảo mã nguồn: Visual Studio Code, WebStorm hoặc Sublime Text.
3. Kiến thức JavaScript cơ bản (biến, hàm, vòng lặp, Promise).

## Cơ chế hoạt động cơ bản

Khi trình duyệt tải trang HTML, nó xây dựng một cây DOM. JavaScript có thể truy cập và thay đổi các phần tử này bằng API chuẩn:

- document — điểm vào để truy vấn và tạo phần tử
- node (Element, Text, Comment, …)
- attributes và textContent / innerText / innerHTML

Ví dụ đơn giản:

```html
<!-- index.html -->
<div id="app">
	<h1>Hello</h1>
	<p class="intro">Welcome</p>
</div>
<script>
	const app = document.getElementById('app');
	console.log(app); // phần tử <div id="app"> …
</script>
```

## Tìm và truy xuất phần tử (Selectors)

1. `getElementById` — truy xuất theo id
```javascript
const el = document.getElementById('myId');
```

2. `getElementsByClassName` / `getElementsByTagName` — trả về HTMLCollection (live)
```javascript
const items = document.getElementsByClassName('item');
```

3. `querySelector` / `querySelectorAll` — hỗ trợ selector CSS; `querySelectorAll` trả về NodeList (static)
```javascript
const first = document.querySelector('.nav li');
const all = document.querySelectorAll('.card');
```

Gợi ý: `querySelector`/`querySelectorAll` rất linh hoạt và được khuyên dùng trong hầu hết trường hợp.

## Thêm / Xóa / Thay thế phần tử

1. Tạo phần tử mới và thêm vào DOM
```javascript
const li = document.createElement('li');
li.textContent = 'Mục mới';
const ul = document.querySelector('#list');
ul.appendChild(li); // thêm vào cuối
```

2. Chèn vào vị trí cụ thể
```javascript
const first = ul.firstElementChild;
ul.insertBefore(li, first); // chèn trước phần tử đầu tiên
```

3. Xóa phần tử
```javascript
const toRemove = document.querySelector('.old');
toRemove.remove(); // hiện đại
// hoặc
toRemove.parentNode.removeChild(toRemove);
```

4. Thay thế phần tử
```javascript
const newNode = document.createElement('div');
newNode.textContent = 'Thay thế';
ul.replaceChild(newNode, ul.children[0]);
```

## Thay đổi nội dung và thuộc tính

- `textContent` — lấy/đặt văn bản thô (an toàn với HTML)
- `innerText` — lấy văn bản hiển thị (tính toán CSS)
- `innerHTML` — lấy/đặt HTML nội bộ (cẩn thận với XSS)

Ví dụ:

```javascript
const p = document.querySelector('.intro');
p.textContent = 'Xin chào!';
p.innerHTML = '<strong>Xin chào!</strong>'; // chèn HTML

// Thuộc tính
p.setAttribute('data-id', '123');
console.log(p.getAttribute('data-id'));
```

## Thay đổi kiểu (Styles) và lớp (classes)

```javascript
const box = document.querySelector('.box');
// Thay đổi style inline
box.style.backgroundColor = 'lightblue';
box.style.padding = '12px';

// Thao tác class
box.classList.add('active');
box.classList.remove('hidden');
box.classList.toggle('open');
```

`classList` là API tiện lợi để quản lý các lớp CSS, tránh thao tác chuỗi qua `className`.

## Event Handling (Xử lý sự kiện)

1. Thêm listener
```javascript
const btn = document.querySelector('#btn');
btn.addEventListener('click', function (event) {
	console.log('Clicked!', event);
});
```

2. Các loại sự kiện phổ biến: `click`, `input`, `change`, `submit`, `keydown`, `DOMContentLoaded`…

3. Event delegation — kỹ thuật tối ưu khi nhiều phần tử con cần xử lý cùng loại sự kiện
```javascript
// thay vì gán cho từng .item, gán cho container
const list = document.querySelector('#list');
list.addEventListener('click', (e) => {
	const item = e.target.closest('.item');
	if (!item) return;
	console.log('Clicked item', item.dataset.id);
});
```

## Form và nhập liệu

1. Ngăn form submit mặc định
```javascript
const form = document.querySelector('#form');
form.addEventListener('submit', (e) => {
	e.preventDefault();
	const data = new FormData(form);
	console.log(Object.fromEntries(data.entries()));
});
```

2. Lấy giá trị trường
```javascript
const value = document.querySelector('input[name="email"]').value;
```

## Tối ưu hiệu năng

1. Giảm reflow/repaint: gom thay đổi DOM vào một lần thao tác (fragment) hoặc dùng `document.createDocumentFragment()`

```javascript
const frag = document.createDocumentFragment();
for (let i = 0; i < 100; i++) {
	const li = document.createElement('li');
	li.textContent = `Item ${i}`;
	frag.appendChild(li);
}
ul.appendChild(frag); // chỉ gây reflow 1 lần
```

2. Debouncing input events để tránh xử lý quá nhiều lần khi người dùng gõ

3. Sử dụng event delegation thay vì gán listener cho từng phần tử con

## Bảo mật — XSS và innerHTML

Khi sử dụng `innerHTML` với dữ liệu từ người dùng, phải cẩn thận vì có thể gây XSS. Thay vì chèn HTML trực tiếp, hãy tạo nodes an toàn bằng `textContent` hoặc sanitize dữ liệu trước khi chèn.

## Các API DOM tiện ích

- `Element.matches(selector)` — kiểm tra phần tử có match selector không
- `Element.closest(selector)` — tìm ancestor gần nhất match selector
- `Node.cloneNode(true)` — clone một node (deep)

## Ví dụ thực tế: Todo List nhỏ

```html
<!-- index.html -->
<form id="todoForm">
	<input name="task" required />
	<button type="submit">Add</button>
</form>
<ul id="todoList"></ul>

<script>
	const form = document.getElementById('todoForm');
	const list = document.getElementById('todoList');

	form.addEventListener('submit', (e) => {
		e.preventDefault();
		const task = form.task.value.trim();
		if (!task) return;

		const li = document.createElement('li');
		li.className = 'item';
		li.textContent = task;

		const removeBtn = document.createElement('button');
		removeBtn.textContent = 'Remove';
		removeBtn.addEventListener('click', () => li.remove());

		li.appendChild(removeBtn);
		list.appendChild(li);
		form.reset();
	});
</script>
```

## Lỗi thường gặp và cách khắc phục

1. `null` khi gọi `querySelector` — kiểm tra rằng selector đúng hoặc DOM đã load (đặt script cuối body hoặc lắng nghe `DOMContentLoaded`).

```javascript
document.addEventListener('DOMContentLoaded', () => {
	// mã thao tác DOM ở đây
});
```

2. Sử dụng `innerHTML` gây XSS — sanitize dữ liệu trước khi chèn.

3. Gán quá nhiều listener gây chậm — dùng event delegation hoặc tái sử dụng listener.

## Bài tập thực hành

1. Xây dựng Todo List có chức năng thêm, xóa, đánh dấu hoàn thành và lưu vào `localStorage`.
2. Tạo bảng lọc (filter) các mục theo từ khóa (live search).
3. Xây một form upload file và hiển thị tiến trình (progress) bằng DOM.

## Công cụ và thư viện hữu ích

- DevTools (Elements, Console, Network)
- jQuery (mặc dù nay ít dùng, nhưng dễ thao tác DOM cho người mới)
- Alpine.js / Stimulus (nhẹ, tương tác DOM theo cách có cấu trúc)

## Kết luận

DOM Manipulation là kỹ năng nền tảng cho lập trình web phía client. Nắm được selectors, DOM API, event handling và các kỹ thuật tối ưu sẽ giúp bạn xây dựng UI tương tác, hiệu năng tốt và an toàn.

## Tài liệu tham khảo

1. MDN: Manipulating documents
	 https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction
2. MDN: Event reference
	 https://developer.mozilla.org/en-US/docs/Web/Events
3. Web.dev: Reflows and repaints
	 https://web.dev/optimize-lcp/

