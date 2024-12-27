# lunar-calendar

农历（阴历）万年历，是一款支持Node.js和浏览器端使用的全功能农历和公历日历类库。支持农历与公历之间相互转换，含有二十四节气，天干地支纪年纪月纪日，生肖属相，公历节假日及农历传统节假日信息等功能。自带2013-2014节假日安排数据，并可自行配置。带有黄历数据，可自行选择配置。支持1891-2100年。使用**lunar-calendar**可快速开发一款属于自己的万年历产品，行动起来吧！

## 安装

### Node.js服务器端(使用npm安装)
```bash
npm install lunar-calendar
```

```bash
pnpm install lunar-calendar
```


```bash
yarn add lunar-calendar
```

### 浏览器端使用，引用脚本
```html
<script type="text/javascript" src="lib/LunarCalendar.min.js"></script>
```

## 使用方法

### Node.js
```javascript
var LunarCalendar = require("lunar-calendar");
```

### 浏览器
`window.LunarCalendar`是一个全局对象，可以全局作用域直接调用。

---

## 方法列表

### 1. `LunarCalendar.calendar(year, month[, fill])`
通过公历获取某月农历数据

#### 参数说明
- `year` (Number): 公历年 范围[1891-2100]
- `month` (Number): 公历月 范围[1-12]
- `fill` (Boolean，可选): 是否填充当月日历首尾日期，设为`true`时，会在首尾填入上下月数据，自动补全一个7x6阵列数据。（可更美观的打造你的万年历产品）

#### 返回数据
```json
{
    "firstDay": 5,
    "monthDays": 28,
    "monthData": [
        {
            "year": 2014,
            "month": 2,
            "day": 1,
            "zodiac": "蛇",
            "GanZhiYear": "癸巳",
            "GanZhiMonth": "乙丑",
            "GanZhiDay": "癸卯",
            "worktime": 2,
            "lunarYear": 2014,
            "lunarMonth": 1,
            "lunarDay": 2,
            "lunarMonthName": "正月",
            "lunarDayName": "初二",
            "lunarLeapMonth": 9,
            "solarFestival": "",
            "lunarFestival": "",
            "term": ""
        },
        ...
    ]
}
```

---

### 2. `LunarCalendar.solarCalendar(year, month[, fill])`
获取公历某月日历数据（不带农历信息）

#### 参数说明
- `year` (Number): 公历年 范围[1-~]
- `month` (Number): 公历月 范围[1-12]
- `fill` (Boolean，可选): 是否填充当月日历首尾日期，设为`true`时，会在首尾填入上下月数据，自动补全一个7x6阵列数据。（可更美观的打造你的万年历产品）

#### 返回数据
```json
{
    "firstDay": 5,
    "monthDays": 28,
    "monthData": [
        {
            "year": 2014,
            "month": 2,
            "day": 1
        },
        ...
    ]
}
```

---

### 3. `LunarCalendar.solarToLunar(year, month, day)`
将公历转换为农历

#### 参数说明
- `year` (Number): 公历年 范围[1891-2100]
- `month` (Number): 公历月 范围[1-12]
- `day` (Number): 公历日 范围[1-31]

#### 返回数据
```json
{
    "zodiac": "蛇",
    "GanZhiYear": "癸巳",
    "GanZhiMonth": "乙丑",
    "GanZhiDay": "癸卯",
    "worktime": 2,
    "lunarYear": 2014,
    "lunarMonth": 1,
    "lunarDay": 2,
    "lunarMonthName": "正月",
    "lunarDayName": "初二",
    "lunarLeapMonth": 9,
    "solarFestival": "",
    "lunarFestival": "",
    "term": ""
}
```

---

### 4. `LunarCalendar.lunarToSolar(year, month, day)`
将农历转换为公历

#### 参数说明
- `year` (Number): 农历年 范围[1891-2100]
- `month` (Number): 农历月 范围[1-13]（有闰月情况，比如当前闰9月，10表示闰9月，11表示10月）
- `day` (Number): 农历日 范围[1-30]

#### 返回数据
```json
{
    "year": 2014,
    "month": 1,
    "day": 31
}
```

---

### 5. `LunarCalendar.setWorktime(data)`
设置某年的节假日安排信息（类库已内置2013-2014年的数据）

#### 参数说明
- `data` (Object): 节假日安排信息(以年为key，可设置多年)

**参数data格式如下**
```javascript
{
    "y2014": {
        "d0101": 2,
        "d0126": 1,
        ...
        "d1011": 1
    }
}
```

---

## 黄历数据
在目录 `/hl/` 下有2008-2020年的黄历数据，用户可自行选择在自己万年历中进行添加。

---

## 公用服务器API
用Node.js搭载lunar-calendar类库。

- **API:** `http://api.tuijs.com/`
- **请求类型:** `GET`
- **返回数据:** JSON 或 JSONP (支持 `callback` 参数).

### API列表
1. 通过公历获取某月农历数据: `/calendar`
2. 获取公历某月日历数据（不带农历信息）: `/solarCalendar`
3. 将公历转换为农历: `/solarToLunar`
4. 将农历转换为公历: `/lunarToSolar`

**例如**
```url
http://api.tuijs.com/lunarToSolar?year=2011&month=1&day=1&callback=fn
```
**返回**
```javascript
fn({"year":2011,"month":2,"day":16})
```

---

## 其它
- **项目主页:** [http://www.tuijs.com/](http://www.tuijs.com/)
- **作者博客:** [http://www.2fz1.com/](http://www.2fz1.com/)
