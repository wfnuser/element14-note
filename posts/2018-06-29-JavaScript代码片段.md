---

title: JavaScript代码片段
date: 2018-06-29

---

## 前言
最近又回前公司实习一段时间，跟谷歌大佬学习一下js的正确打开方式。

* reduce

    ```
    const KEYS = {
        'r': 'referralCode',
    }

    /**
    * _.invert(KEYS)
    * @type {!Object<string, string>}
    */
    const NAMES = Object.keys(KEYS).reduce((prev, curr) => {
    prev[KEYS[curr]] = curr
    return prev
    }, {})
    ```

