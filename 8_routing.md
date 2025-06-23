# 📘 (React Router v6+)

## 1. ✅ Routing là gì?

Routing là cách React "điều hướng" giữa các trang trong Single Page Application (SPA) mà **không reload toàn bộ trang web**.

---

## 2. 🔧 Cài đặt React Router

```bash
npm install react-router-dom
```

---

## 3. 📦 Các khái niệm chính trong React Router

| Tên             | Vai trò                                         |
| --------------- | ----------------------------------------------- |
| `BrowserRouter` | Bốc ngoài toàn app, quản lý URL                 |
| `Routes`        | Bao quanh các route con                         |
| `Route`         | Khai báo đường dẫn và component tương ứng       |
| `Link`          | Thay thế cho thẻ `<a>` nhưng không reload trang |
| `useNavigate`   | Điều hướng bằng code (JS)                       |
| `useParams`     | Lấy tham số đường dẫn                           |
| `Outlet`        | Render route con trong layout cha               |

---

## 4. 🛠 Cách dùng cơ bản

### Cấu trúc routing:

```jsx
import { BrowserRouter, Routes, Route, Link } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## 5. 🧭 useNavigate - Điều hướng qua JS

```jsx
import { useNavigate } from "react-router-dom";

const Login = () => {
  const navigate = useNavigate();

  const handleLogin = () => {
    // Sau khi login thành công
    navigate("/dashboard");
  };

  return <button onClick={handleLogin}>Login</button>;
};
```

---

## 6. 🔧 useParams - Truy xuất tham số trong URL

```jsx
// Định nghĩa route
<Route path="/user/:id" element={<UserDetail />} />;

// Truy cập params trong component
import { useParams } from "react-router-dom";

function UserDetail() {
  const { id } = useParams();
  return <div>User ID: {id}</div>;
}
```

---

## 7. 🧩 Nested Routes (Route lồng nhau)

```jsx
<Route path="/dashboard" element={<DashboardLayout />}>
  <Route path="stats" element={<Stats />} />
  <Route path="settings" element={<Settings />} />
</Route>
```

Trong `DashboardLayout` cần có `Outlet`:

```jsx
import { Outlet } from "react-router-dom";

function DashboardLayout() {
  return (
    <div>
      <Sidebar />
      <Outlet />
    </div>
  );
}
```

---

## 8. ❌ Route 404 Not Found

```jsx
<Route path="*" element={<NotFound />} />
```

---

## 9. 🛡 Route Protection (Private Routes)

```jsx
function PrivateRoute({ children }) {
  const isAuth = useAuth();
  return isAuth ? children : <Navigate to="/login" />;
}

<Route
  path="/dashboard"
  element={
    <PrivateRoute>
      <Dashboard />
    </PrivateRoute>
  }
/>;
```

---

## 10. 📚 Tóm tắt

- Dùng `BrowserRouter` bọc ngoài
- `Routes` bao quanh các `Route`
- `Link` thay cho thẻ `<a>`
- Dùng `useNavigate`, `useParams`, `Outlet` cho logic linh hoạt
- Nested route, 404, route protection là những kỹ thuật quan trọng
