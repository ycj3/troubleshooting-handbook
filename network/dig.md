## 基本用途

用于查询域名解析记录（A、CNAME、MX 等），验证 DNS 是否被劫持。

## 常用命令

```
dig example.com
dig @8.8.8.8 example.com
dig +trace example.com
```

## 输出解读

| 字段           | 命令                  |
| -------------- | --------------------- |
| ANSWER SECTION | 域名解析结果          |
| Query time     | DNS 查询耗时          |
| SERVER         | 实际响应的 DNS 服务器 |

## 延伸阅读

- [RFC 1035 — DNS Protocol](https://www.rfc-editor.org/rfc/rfc1035)
- [Google Public DNS Docs](https://developers.google.com/speed/public-dns)
