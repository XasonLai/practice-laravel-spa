# My SPA with Laravel 練習

## 項目簡介

這是一個使用 Laravel 和 Vue.js 構建的單頁應用（SPA）。該項目旨在展示如何將前端框架與後端框架結合，創建一個現代化的 Web 應用。

## 安裝和設置

### 前置條件

- PHP >= 7.4
- Composer [Composer 安裝](https://getcomposer.org/download/)
- Node.js & npm [NodeJS 安裝](https://nodejs.org/zh-cn)


## 過程記錄

### 1. 安裝 Laravel
``` cmd
composer create-project --prefer-dist laravel/laravel practice-spa
```

### 2. 安裝前端框架 (VUE)
``` cmd
npm install vue vue-router @vitejs/plugin-vue
```

### 3. 配置 Vite
編輯 `vite.config.js` 文件，添加 Vue 插件:
```js
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import vue from '@vitejs/plugin-vue';

export default defineConfig({
    plugins: [
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
        vue(),
    ],
});
```

### 4. 設置 Vue 應用
在 `resources/js` 目錄中創建一個 `app.js` 文件，並初始化 Vue 應用:
```js
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';

createApp(App).use(router).mount('#app');
```

創建 `App.vue`:
```js
<template>
  <div id="app">
    <header>
      <nav>
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
      </nav>
    </header>
    <main>
      <router-view></router-view>
    </main>
    <footer>
      <p>© 2024 My Vue App</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>
/* 全局樣式 */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

nav a {
  margin: 0 10px;
  color: #42b983;
  text-decoration: none;
}

nav a.router-link-exact-active {
  font-weight: bold;
}
</style>

```

### 5. 設置 Vue 路由
在 `resources/js` 目錄中創建一個 `route.js` 文件來配置 Vue 路由:
```js
import { createRouter, createWebHistory } from 'vue-router';

const routes = [
    {
        path: '/',
        name: 'Home',
        component: () => import('./components/Home.vue'),
    },
    {
        path: '/about',
        name: 'About',
        component: () => import('./components/About.vue'),
    },
];

const router = createRouter({
    history: createWebHistory(),
    routes,
});

export default router;
```

### 6. 創建 Vue 組件
在 `resources/js/components` 目錄中創建 `Home.vue` 跟 `About.vue`:

Home.vue:
```js
<template>
  <div>
    <h1>Home Page</h1>
  </div>
</template>

<script>
export default {
  name: 'Home',
};
</script>

<style scoped>
/* 你的樣式 */
</style>
```

About.vue
```js
<template>
  <div>
    <h1>Home Page 1111</h1>
  </div>
</template>

<script>
export default {
  name: 'Home',
};
</script>

<style scoped>
/* 你的樣式 */
</style>
```

### 7. 配置 Blade
在 `resources/views` 目錄中編輯 `welcome.blade.php` 文件，將其設置載入 Vue 應用:
```html
<!DOCTYPE html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Laravel</title>
    @vite('resources/js/app.js')
</head>
<body>
    <div id="app"></div>
</body>
</html>

```

### 8. 路由
確保 Laravel 的路由配置允許 Vue Router 處理 SPA 路由。在 routes/web.php 中添加一個 catch-all 路由：
```php
Route::get('/{any}', function () {
    return view('welcome');
})->where('any', '.*');
```

### 9. 編譯前端資源
```cmd
npm run dev
```

### 10. 啟動伺服器
```cmd
php artisan serve
```

打開瀏覽器並訪問 http://localhost:8000 查看應用。

---
以上是作練習使用，多數是請教於 Chat GPT，如果有相關問題，歡迎聯繫；如果有錯誤的話，也歡迎聯繫告知，謝謝。