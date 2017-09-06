---

title: DataV & QuickBI & ARMs 数据展示平台调研
date: 2017-09-06

---


# DataV
## 发布
企业版支持加密发布和动态token鉴权 详见 [DataV 支持 token 验证啦！](https://yq.aliyun.com/articles/69394?spm=0.0.0.0.B7GJKo)
## 数据源配置
* 数据库类
    * Analytic DB
    * RDS for MySQL
    * RDS for PostgreSQL
    * RDS for SQLServer·
    * Hybrid DB
    * Oracle
    * 兼容 MySQL 数据库
* 文件类
    * JSON
    * CSV
* API类
    * POP API
    * 阿里云 API 网关
* 其他
    * DataV数据库代理服务

数据自动更新方案为定时查询

# Quick BI
## 发布·
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