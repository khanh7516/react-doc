## State

**State** là một đối tượng chứa **dữ liệu nội tại (internal)** của một component. Khi state thay đổi, **component sẽ tự động re-render** để cập nhật giao diện.

---

## 🧠 Đặc điểm của State

- **Thuộc về component** (local state).
- **Không truyền được xuống component con** (phải truyền qua props).
- **Có thể thay đổi bằng `setState`**.
- Khi state thay đổi → component sẽ **tự động re-render**.
- **Không được thay đổi trực tiếp** (phải dùng `setState`).
- toàn bộ giao diện hiển thị đều được là đại diện cho state hiện tại theo thời gian

---

## 🛠️ Cách dùng state (React Hook)

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // khởi tạo state

  const increase = () => {
    setCount(count + 1); // cập nhật state
  };

  return (
    <div>
      <p>Giá trị: {count}</p>
      <button onClick={increase}>Tăng</button>
    </div>
  );
}
```

| Thuộc tính                 | State                                    | Props                |
| -------------------------- | ---------------------------------------- | -------------------- |
| Tạo ở đâu?                 | Bên trong component                      | Ở component cha      |
| Ai thay đổi được?          | Chính component                          | Component cha        |
| Có thay đổi được không?    | ✅ Có                                    | ❌ Không (read-only) |
| Làm thay đổi UI?           | ✅ Có                                    | ✅ Có                |
| Truyền cho component khác? | ✅ Có (thông qua props, không trực tiếp) | ✅ Có thể qua props  |
