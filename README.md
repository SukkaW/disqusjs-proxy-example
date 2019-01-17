# disqusjs-proxy-example

一个使用 [ZEIT Now](https://zeit.co/) 部署 Disqus API Proxy 的示例。

## 简介

ZEIT Now 提供 Serverless 部署服务，支持包括静态网页、微服务、Lambda、持续集成等。在这里我们使用 Now 的微服务功能部署一个 Disqus API 的反代。

[DisqusJS](https://github.com/SukkaW/DisqusJS) 中提供的公共 Disqus API 反代就部署在 ZEIT Now 上。

## 使用教程

1. fork 这个 repo
2. 在 [ZEIT](https://zeit.co/) 上注册账号并绑定 GitHub 账号
3. 在 [GitHub APP](https://github.com/settings/installations) 中为 Now 设置你 fork 后的 repo 的访问权限
4. 在你 fork 后的 repo 中修改 `_now.json` 的相关内容
  - 如果你想要绑定你自己的域名，请将 `_now.json` 中 `[Place Your Domain Here]` 改成你的域名，否则你可以将整个 `alias` 字段删除
  - 如果不配置自己的域名，你也可以使用 ZEIT 提供的 `now.sh` 子域名
  - 将 `[Cache Age]` 修改为缓存时长（数字），单位是秒。如果你并不需要设置 `Cache-Control` 响应头，你可以将 `routes.headers` 字段删除
  - 如果你想要定制其它内容（如添加响应头），请参阅 [ZEIT 的相关文档](https://zeit.co/docs/v2/deployments/configuration/)
5. 将 `_now.json` 重命名为 `now.json` 并提交 commit
6. ZEIT 会自动开始部署你的项目，当部署完成后，ZEIT 的 Bot 会在你的 commit 中添加一条评论提示部署结果
7. 如果你绑定了你自己的域名，需要添加一条 `CNAME` 记录指向 `alias.zeit.co`
8. 测试你的反代是否可以使用：访问你的反代域名，应该会跳转到 Disqus API 文档页面
  > 因为直接访问 https://disqus.com/api/ 便会跳转到 https://disqus.com/api/docs/ ；反代也会返回 3xx 状态码
9. 修改你的服务中 Disqus API Endpoint 的配置；如果你正在使用 [DisqusJS](https://github.com/SukkaW/DisqusJS)，这个配置是 DisqusJS 中的 `api` 字段。

## 注意事项

- ZEIT 提供永久免费的 Plan，但是有 100GB 的流量限制
- ZEIT 实例中的 `now.sh` 域名会使用 Cloudflare 的 Enterprise Plan；但是你绑定的自己的域名只能使用 ZEIT 自有的基础设施，如有必要可以在 Now 实例之外套一层 CDN
