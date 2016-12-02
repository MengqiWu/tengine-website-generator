# ngx_http_upstream_dynamic_module

此模块提供了在运行时动态解析upstream中server域名的功能。

```
upstream backend {
    dynamic_resolve fallback=stale fail_timeout=30s;

    server a.com;
    server b.com;
}

server {
    ...

    location / {
        proxy_pass http://backend;
    }
}
```

## 指令

> Syntax: **dynamic_resolve** [fallback=stale|next|shutdown] [fail_timeout=time]
> Default: -
> Context: upstream.


指定在某个upstream中启用动态域名解析功能。

fallback参数指定了当域名无法解析时采取的动作：

    fail_timeout参数指定了将DNS服务当做无法使用的时间，也就是当某次DNS请求失败后，假定后续多长的时间内DNS服务依然不可用，以减少对无效DNS的查询。

