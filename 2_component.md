### Component

- Gồm data + logic + appearance
- Khối UI độc lập để tái sử dụng VD: nút bấm, thẻ bài viết, form, ...
- Giúp chia nhỏ UI cho dễ quản lý, tái sử dụng
- Nằm trong file tsx, jsx (react), là 1 lá của toàn bộ app
- lib react giúp quản lý component

```jsx
function Button({ label }) {
  return <button>{label}</button>;
}

// Sử dụng
<Button label="Click me" />;
```

### Declarative component

- Mô tả các Components trông như thế nào bằng 1 cú pháp gọi là JSX
- ReactJS sẽ biết 1 Component trông như thế nào dựa trên các data + state hiện tại
- Không cần động vào dom

### JSX/ TSX

- Là cú pháp mở rộng của js/ts cho phép viết HTML bên trong.

```jsx
const element = <h1>Hello, world!</h1>;
```

### State-driven

- UI của component được điều khiển bởi state
- state thay đổi -> UI thay đổi

### Component cha và con

- Parent: component ngoài chứa các component khác
- Child: component trong 1 component khác

```jsx
// Welcome.jsx - Component con
function Welcome({ name }) {
  return <h1>Xin chào, {name}!</h1>;
}

// App.jsx - Component cha
function App() {
  return <Welcome name="Khánh" />;
}
```

### Component composition

- kỹ thuật kết hợp nhiều component nhỏ để tạo nên component lớn hơn.

VD:

```jsx
function Layout({ header, content, footer }) {
  return (
    <>
      <header>{header}</header>
      <main>{content}</main>
      <footer>{footer}</footer>
    </>
  );
}

function App() {
  return (
    <Layout
      header={<h1>Tiêu đề</h1>}
      content={<p>Nội dung trang</p>}
      footer={<small>Bản quyền</small>}
    />
  );
}
```

### Pure Component

- Không thay đổi dữ liệu bên ngoài (props, biến global…)
- Không tạo side effect (như gọi API, setTimeout, ghi localStorage…)
- Chỉ phụ thuộc vào props và state để tạo ra JSX
- Mỗi lần render cùng một input, luôn trả về cùng một output
