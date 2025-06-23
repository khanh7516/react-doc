### Tại sao cần Redux?

React quản lý state cục bộ bằng useState. Nhưng khi app lớn lên, có nhiều vấn đề:

- "Props drilling" khi truyền dữ liệu qua nhiều cấp

- Nhiều component cần dùng chung 1 state (ví dụ: user login, theme, giỏ hàng)

- Khó theo dõi luồng dữ liệu

=> Redux sinh ra để giải quyết việc quản lý state toàn cục một cách có tổ chức và dễ kiểm soát.

### Redux gồm

| Thành phần   | Giải thích ngắn                         |
| ------------ | --------------------------------------- |
| **Store**    | Nơi lưu trữ state toàn cục              |
| **Action**   | Mô tả "chuyện gì đã xảy ra"             |
| **Reducer**  | Quyết định "cập nhật state như thế nào" |
| **Dispatch** | Gửi action đến reducer                  |
| **Selector** | Lấy state ra từ store                   |

### Luồng hoạt động

```
UI (button click, input...)
   ↓ dispatch(action)
Action (type, payload)
   ↓
Reducer (nhận action + state cũ → trả về state mới)
   ↓
Store cập nhật
   ↓
UI tự động render lại
```

### Ví dụ

- Khởi tạo store

```js
// counterSlice.js
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    addByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, addByAmount } = counterSlice.actions;
export default counterSlice.reducer;
```

- Kết hợp reducers vào store

```js
// store.js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

- Dùng redux trong component

```js
// Counter.jsx
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement, addByAmount } from "./counterSlice";

function Counter() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(decrement())}>-</button>
      <button onClick={() => dispatch(addByAmount(5))}>+5</button>
    </div>
  );
}
```
