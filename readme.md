# OpenApi Traefik中间件

请求地址： /open_api/{目标系统标识}/{目标系统路由}?{请求参数}  
请求头：
- X-OpenApi-SN 本系统标识  
- X-OpenApi-Authtype 授权类型(ticket\sign)  
前端调用：
- X-OpenApi-Ticket [ticket生成指南](#ticket生成指南)
- X-OpenApi-ExpireTime ticket过期时间（时间戳，秒级）
- X-OpenApi-AllowSn ticket授权信息  
后端调用：
- X-OpenApi-Sign [sign生成指南](#sign生成指南)
- X-OpenApi-Nonce 随机数，建议8位
- X-OpenApi-Timestamp 时间戳，秒级
- X-OpenApi-SignPara 需要签名的参数(--暂未实现)

## 功能
- 记录OpenApi请求日志
- OpenApi鉴权

### ticket生成指南
ticket = md5 32位小写([X-OpenApi-AllowSn]+[X-OpenApi-ExpireTime]+[SystemSecret])

### sign生成指南
sign = md5 32位小写([X-OpenApi-Nonce]+[X-OpenApi-Timestamp]+[SystemSecret])