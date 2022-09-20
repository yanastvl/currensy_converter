<h1 align="center">Currency Converter</h1>

## SPA для конвертирования валют.
<p>Использовано API ЦБ РФ https://cdn.cur.su/api/cbr.json.</p>
<p>Цель приложения:</p>
<p>Дать пользователю возможность конвертировать из одной валюты в другую.</p>

##
#### 1. Приложение состоит из:
  - поле для ввода суммы в валюте, из которой конвертирует пользователь (базовой)
  - выбор базовой и целевой валюты (в которую конвертирует пользователь)
  - поле результата
#### 2. По умолчанию у пользователя определяется базовая валюта, соответствующая локали браузера.
#### 3. Конвертация происходит сразу после ввода суммы в базовой валюте, на лету.

![image (1)](https://user-images.githubusercontent.com/87431718/191267355-b02b5b34-59bc-4660-845e-a2baed41994d.png)


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```


### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
