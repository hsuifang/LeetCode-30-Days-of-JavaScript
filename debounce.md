# 2627 Debounce
#JavaScript #Debounce #setTimeout #scope #closure

## 題目說明 Brief
> 傳入`fn` 及 `t`毫秒為單位的的時間，並返回一個 debounced 版本的函數

一個 debounced 的函數是一個延後 t毫秒才執行的函數
如果在這期間，又再被呼叫，則取消該執行。
假設 t = 50ms，函數在 30ms、60ms 和 100ms 被呼叫。前兩次函數呼叫將被取消。

## 直覺 Intuition
Debounce 的核心思想是使用 setTimeout 
當函數被連續多次呼叫時，前面的計時器會被清除，也就是重置了計時器。
這個過程確保了函數只在最後一次呼叫後的特定時間框架內被執行一次。

## 實現方法 Approach
- **建立一個 `debounce` 的 function**: 接受兩個參數 - `fn` 及 `t`
- **初始化計時器**：建立一個儲存計時器 `timeoutID` 的變數
- **返回一個新function**： debounce function 返回一個新的function 。這個新function 將代替原始function 被呼叫使用
- **重置計時器**：每次呼叫函數時，透過 `clearTimeout(timeoutID)` 清除任何現有的計時器
- **延遲函式執行**： 透過 `setTimeout` 將執行function的時機延遲至指定的時間間隔
- **在最後一次呼叫後執行函數**：一旦指定的時間過去而沒有新的呼叫，原始函數就會被執行。

## Code
```
/**
 * @param {Function} fn - 要被防抖的函數。
 * @param {number} t - 防抖時間，以毫秒為單位。
 * @return {Function} - 防抖後的函數。
 */
var debounce = function(fn, t) {
    let timer;
    return function(...args) {
        clearTimeout(timer);
        timer = setTimeout(() => {
            fn.apply(this, args);
        }, t);
    };
};
```
---


## 相關觀念
- Scope 
- Closure
- setTimeout