### Hook?

- Hooks là các hàm đặc biệt có sẵn trong React
- Móc vào bên trong react để:
  - truy cập, cập nhật state
  - thực hiện sideEffect
  - truy cập trực tiếp dom (useRef)
  - ...
- Phải gọi ở top-level và trong function component

VD:
Chỉ gọi Hook ở cấp cao nhất (top level)

- ❌ Sai (gọi trong điều kiện):

```js
function MyComponent() {
  if (someCondition) {
    const [count, setCount] = useState(0); // ❌ KHÔNG ĐƯỢC
  }

  return <div>Example</div>;
}
```

- ✅ Đúng:

```js
function MyComponent() {
  const [count, setCount] = useState(0); // ✅ Gọi trực tiếp

  if (someCondition) {
    // Có thể dùng count ở đây
  }

  return <div>Example</div>;
}
```

Chỉ gọi Hook trong function component hoặc custom hook

- ❌ Sai (gọi trong hàm thường):

```js
function doSomething() {
  const [count, setCount] = useState(0); // ❌ KHÔNG ĐƯỢC
}

function MyComponent() {
  doSomething();

  return <div>Example</div>;
}
```

- ✅ Đúng (gọi trong component hoặc custom hook):

```js
function MyComponent() {
  const [count, setCount] = useState(0); // ✅ OK

  return <div>{count}</div>;
}
```

Hoặc

```js
function useMyHook() {
  const [count, setCount] = useState(0); // ✅ OK trong custom hook
  return [count, setCount];
}

function MyComponent() {
  const [count, setCount] = useMyHook(); // ✅ OK
  return <div>{count}</div>;
}
```

### useState

- 1 hook cơ bản để quản lý trạng thái
- Khởi tạo:

  - simple

  ```js
  const [count, setCount] = useState(23);
  ```

  - Lazy Initialization

  ```js
  const [count, setCount] = useState(() => LocalStorage.getItem("count"));
  ```

- Cập nhật:

  - simple:

  ```js
  setCount(1000);
  ```

  - Dựa trên state hiện tại:

  ```js
  setCount((c) => c + 1);
  ```

### useEffect

- useEffect() dùng để thực hiện các side effects trong React sau khi render.
- useEffect(callback,[depns]): callback là bắt buộc, depns là không bắt buộc
- Không cần cleanUp: API, thao thác DOM
- Cần cleanUp: time out
- Cách thức hoạt động của useEffect
  - Callback luôn được gọi sau khi component Mount
  - Cleanup Fn (dọn dẹp) luôn được gọi trước khi component Unmount
  - Cleanup luôn được gọi trước callback mỗi lần re-render ( trừ trường hợp mouted)
  - Thời điểm được gọi là sau khi component đã được gắn vào DOM
  - Callback không có depens
    - Callback se được gọi lúc component mount và bất cứ khi nào component bị rerender
  - Callback với depens rỗng
    - Chỉ gọi callback 1 lần sau khi component được Mounted
  - Callback với depens
    - Callback sẽ được gọi mỗi khi depens thay đổi
  - Cleanup Fn
    - Luôn được gọi trước khi callback mới được gọi
    - Luôn được gọi trước khi component Unmount

### useReducer

- quản lý state phức tạp (state là obj hoặc nhiều giá trị)
- Cú pháp

```js
const [state, dispatch] = useReducer(reducerFn, initialState);
```

VD:

```js
const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "reset":
      return { count: 0 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "reset" })}>Reset</button>
    </>
  );
}
```

### useContext() - Truyền dữ liệu toàn ứng dụng

- Tránh truyền props nhiều cấp (prop drilling)
- Dùng cho theme, auth, language, user, config

```js
const ThemeContext = React.createContext();

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Page />
    </ThemeContext.Provider>
  );
}

function Page() {
  const theme = useContext(ThemeContext);
  return <h1>Current theme: {theme}</h1>;
}
```

### useRef() – Tham chiếu DOM hoặc giữ giá trị không re-render

- Truy cập DOM node hoặc Lưu biến mà không gây render lại khi thay đổi

VD: useRef = biến "ẩn" không ảnh hưởng render – rất hữu ích!

```js
const prevCount = useRef();
useEffect(() => {
  prevCount.current = count;
});
```

### useCallback()

- giúp ghi nhớ lại một function giữa các lần render ⇨ tránh tạo lại ⇨ tránh render lại không cần thiết

### custom hook

- Custom Hook = một function tự viết nhưng dùng hook bên trong (useState, useEffect, v.v.).

- Khi bạn có logic có dùng hook và muốn tái sử dụng ở nhiều component.

VD:

```js
function useFetch(url) {
  const [data, setData] = useState([]);
  const [isLoading, setIsLoading] = useState(false);

  useEffect(() => {
    setIsLoading(true);
    fetch(url)
      .then((res) => res.json())
      .then((data) => {
        setData(data);
        setIsLoading(false);
      });
  }, [url]);

  return [data, isLoading];
}
```

```js
function App() {
  const [data, isLoading] = useFetch("https://api.example.com/users");

  return (
    <>
      {isLoading ? "Loading..." : data.map(...)}
    </>
  );
}

```

- Bắt đầu bằng use (useFetch)

- Dùng hook bên trong (useState, useEffect)

- Trả về dữ liệu cần thiết (ở đây là data và isLoading)

- Không chứa UI → chỉ chứa logic (hook chỉ là logic)
