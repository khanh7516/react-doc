### Context

- dùng để truyền dữ liệu sâu xuống các component con mà không cần phải truyền props qua từng cấp

- Các tình huống thường dùng:

  - Chủ đề giao diện (theme: light/dark)

  - Người dùng đang đăng nhập (auth)

  - Ngôn ngữ (i18n)

  - Cài đặt toàn cục

  - Dữ liệu giỏ hàng, trạng thái toàn app, v.v.

| Mục đích  | Truyền dữ liệu toàn cục mà không cần props |
| --------- | ------------------------------------------ |
| Tạo bởi   | `createContext()`                          |
| Truy cập  | `useContext(MyContext)`                    |
| Phải dùng | `<MyContext.Provider value={...}>`         |

Lưu ý

- Không nên lạm dụng context cho dữ liệu thay đổi liên tục (như input, mouse position) vì sẽ gây re-render toàn bộ cây context.

- Nên chia nhỏ context theo từng mục đích cụ thể (theme, auth, settings...) để tránh render không cần thiết.

#### Cách dùng context

- Tạo Context

```js
import { createContext } from "react";

export const ThemeContext = createContext();
```

- Tạo provider

```js
import { useState } from "react";
import { ThemeContext } from "./ThemeContext";

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export default ThemeProvider;
```

- Dùng trong App

```js
import ThemeProvider from "./ThemeProvider";

function App() {
  return (
    <ThemeProvider>
      <YourComponent />
    </ThemeProvider>
  );
}
```

- Dùng dữ liệu context trong các component

```js
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

function YourComponent() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <div>
      Current theme: {theme}
      <button onClick={() => setTheme(theme === "light" ? "dark" : "light")}>
        Toggle theme
      </button>
    </div>
  );
}
```
