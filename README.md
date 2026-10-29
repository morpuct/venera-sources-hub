# Venera 漫画源合订索引

汇总官方与社区 8 个仓库的漫画源，每一条都指向**原作者仓库里的原文件**；本仓库只存索引，不复制任何源码。

## 三份清单

| 文件 | 条目 | 说明 |
|---|---|---|
| `index.all.json` | **61** | **合集**：筛选去重后的全部站点，含 13 条需代理（`description` 注明） |
| `index.verified.json` | 48 | 只含直连可拉取的（含 Komga/Kavita/Lanraragi 自建书库） |
| `index.proxy.json` | 13 | 仅有代理需求的 |
| `index.json` | 105 | 全量：8 仓合并未筛选，含同一站点的多个实现，排查用 |

在 Venera / 漫阅 里“添加源链接”填：

```
https://cdn.jsdelivr.net/gh/morpuct/venera-sources-hub@main/index.all.json
```

> jsdelivr 对 `@main` 有缓存，刚更新过仓库时可能仍返回旧版；要确定内容用 `@<commit>` 或 `https://raw.githubusercontent.com/morpuct/venera-sources-hub/main/index.all.json`。

## 收录来源

| 来源仓库 | 全量 105 中的条数 |
|---|---|
| venera-app/venera-configs | 33（官方基线） |
| Junkrat9527/venera-sources | 65 |
| LX7kM9/venera-configs | 3 |
| JunQianNuo/venera-sources | 2 |
| maplessovo/venera-configs | 1 |
| 940440952/comic-sources | 1 |

## 筛选口径

1. 从每个源脚本里抽主域名（`baseUrl` 声明 → settings 默认域名 → 出现最多的非 CDN 域名）
2. 在北京联通家宽直连下抓站点首页（`curl -L -m 15`），检测 `challenge_required`、`cf-chl`、`Just a moment`、`__gatekeeper` 等验证特征
3. 直连失败的再经代理复核，区分“需代理”与“真不可用”
4. 同一站点（根域名或名称相同）只保留一条：先看可用档位，再优先官方版本

结果（85 个站点）：直连快 34、直连但慢 11、需代理 13、站点校验 3、不可用 21、自建书库 3。

**局限**：测的是站点首页，不是源实际调用的接口。首页通只说明站点活着，详情页仍可能被二次校验拦下。例如官方包子源指向 `cn.bzmgcn.com`（302 → `www.baozimh.com`，403 `challenge_required`），而 JunQianNuo 的 `baozi_fixed.js` 走 `cn.webmota.com` 实测 200，筛选版保留的是后者。

## 注意

- 版本号由各仓库自行编写，**大小不代表新旧**，同一文件在官方是 1.4.3、在聚合库可能被写成 2.3.0。
- 部分源需要登录、邀请码或地区网络（索引里保留了原作者的说明文字）。
- 源脚本的版权归各原作者，本仓库只做索引聚合；如原作者要求移除某条，删对应行即可。

生成时间：2026-10-28
