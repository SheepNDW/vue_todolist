# TodoList 案例

![image](https://raw.githubusercontent.com/SheepNDW/vue_todolist/master/src/sampleGif/todolist.gif)

## 概要

以腳手架(Vue CLI )開發一個可以進行增､刪､改並帶有本地儲存功能(LocalStorage)的 TodoList 案例

## 使用技術

1. 拆分成 4 個組件實現組件化開發
2. 使用 props 傳遞 todos 資料給各組件
3. 使用自定義事件實現子組件給父組件傳遞傳資料
4. 使用全局事件總線（\$bus）實現組件間的互相傳遞
5. 利用\$nextTick 達成自動焦點
6. 將代辦事項儲存在 LocalStorage
7. 套用第三方庫 Animate.css 為案例添加動畫效果
