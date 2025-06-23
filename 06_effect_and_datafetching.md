### THE COMPONENT LIFECYCLE

mount -> re-render (optional) -> ummount

- mount: component is rendered for the first time
- re-render: when state changes, props change, parent re-renders, context changes
- un-mount: component is destroyed, state or prop are destroyed

### Side Effect

- Thực thi những logic ngoài logic render UI

| `useEffect(() => {})`               | Chạy sau mỗi lần render              |
| ----------------------------------- | ------------------------------------ |
| `useEffect(() => {}, [])`           | Chạy **một lần** khi mount           |
| `useEffect(() => {}, [dep1, dep2])` | Chạy khi `dep1` hoặc `dep2` thay đổi |

VD:

- Gọi API khi component load:

```js
useEffect(() => {
  fetch("/api/data")
    .then((res) => res.json())
    .then((data) => setData(data));
}, []);
```

- Theo dõi thay đổi biến (deps):

```js
useEffect(() => {
  console.log("Giá trị count đã thay đổi:", count);
}, [count]);
```

- Cleanup effect (khi component unmount):

```js
useEffect(() => {
  const intervalId = setInterval(() => {
    console.log("Tick");
  }, 1000);

  return () => {
    clearInterval(intervalId); // Dọn dẹp khi component biến mất
  };
}, []);
```
