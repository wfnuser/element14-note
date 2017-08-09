---

title: DataV & QuickBI & ARMs 数据展示平台调研
date: 2017-07-20

---


# DataV
## 发布
基础版只支持公开发布
企业版支持加密发布和动态token鉴权 详见 [DataV 支持 token 验证啦！](https://yq.aliyun.com/articles/69394?spm=0.0.0.0.B7GJKo)

# Quick BI
## 发布
高级版未出，不支持token

# ARMs
## 环比功能
未发，近期上线。
## 监控功能
集团内部支持可单独配置。 Tsar监控近期会开放白名单，公有云上也可以用。
## 数据源支持
* LogHub （LogService）
* ECS
* SDK
* MQ
* DRDS（未发）
## 问题
累积求和支持不好，只能做固定时间区间内求和，目前最长为1个月。数据流间断，则不记录。