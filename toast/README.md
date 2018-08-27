# toast-vue-mobile


> toast-vue-mobile
  vue2.0


### 1. Install
```sh
$ npm install toast-vue-mobile
```
----


### 2. Usage


> **toasts(ref="toasts", :type='toastIcon', :show='toastShow')**


### 3. props


| name        | type   |  default  | required |
| --------   | -----:  | :----:  | -----: |
| show     | Boolean |   true   | false
| type     | String |   toastText   | false
| timeout     | Number |   1600   | false
| text     | String |   正在提交   | false


### 4. methods

|  function name        | argument   | description
| --------   | -----:  | :----:  |
| getType     | type = toastText,toastIcon |      type
| showToast     | @param text, timeout|      @returns {Promise}

### 5. demo
#### props type is 'toastIcon':
![toastText](./img/icon.gif)
---
#### props type is 'toastText':
![toastIcon](./img/text.gif)

---
License
----

MIT

