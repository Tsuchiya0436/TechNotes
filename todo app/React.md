## React環境の設定
### 1. プロジェクトの作成
``` bash  
npx create-react-app todo-app
cd todo-app
npm start
```
※ npmではプロジェクト名の命名ルーツとして、大文字を含めることを禁止している。

---

### 2. taskの保存と追加機能を追加(`src/App.js`)
``` js
import React, { useState } from 'react';

function App() {
  const [task, setTask] = useState('');
  const [tasks, setTasks] = useState([]);

  const addTask = () => {
    if (task.trim() !== '') {
      setTasks([...tasks, task]);
      setTask('');
    }
  };

  return (
    <div style={{ padding: '20px' }}>
      <h1>ToDoアプリ</h1>
      <input
        type="text"
        value={task}
        onChange={(e) => setTask(e.target.value)}
        placeholder="新しいタスクを追加"
      />
      <button onClick={addTask}>追加</button>

      <ul>
        {tasks.map((t, index) => (
          <li key={index}>{t}</li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```
<br>  

`import`文
``` js
import React, { useState } from 'react';
```
Reactを使うためにインポートをする。  
`useState`はReactのフック(機能の１つ)で、コンポーネントが持つデータを動的に管理できる。
<br>  
`App`コンポーネント
``` js
function APP() {
}
```