### React 自定义hooks

#### 使用自定义hooks

> 自定义 Hook 是一个函数，其名称以 “use” 开头，函数内部可以调用其他的 Hook。
> 
> 自定义 Hook 是一种自然遵循 Hook 设计的约定，而并不是 React 的特性。
> 
> 自定义 Hook 必须以 “use” 开头吗？必须如此。
> 
> 在两个组件中使用相同的 Hook 会共享 state 吗？不会。自定义 Hook 是一种重用状态逻辑的机制(例如设置为订阅并存储当前值)，所以每次使用自定义 Hook 时，其中的所有 state 和副作用都是完全隔离的。
> 
> 自定义 Hook 如何获取独立的 state？每次调用 Hook，它都会获取独立的 state。由于我们直接调用了 useFriendStatus，从 React 的角度来看，我们的组件只是调用了 useState 和 useEffect。
> 

#### 例子

自定义：useFriendStatus

```js
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

使用

```js
const friendList = [
  { id: 1, name: 'Phoebe' },
  { id: 2, name: 'Rachel' },
  { id: 3, name: 'Ross' },
];

function ChatRecipientPicker() {
  const [recipientID, setRecipientID] = useState(1);
  const isRecipientOnline = useFriendStatus(recipientID);

  return (
    <>
      <Circle color={isRecipientOnline ? 'green' : 'red'} />
      <select
        value={recipientID}
        onChange={e => setRecipientID(Number(e.target.value))}
      >
        {friendList.map(friend => (
          <option key={friend.id} value={friend.id}>
            {friend.name}
          </option>
        ))}
      </select>
    </>
  );
}
```