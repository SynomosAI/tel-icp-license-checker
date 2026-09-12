# tel-icp-license-checker

> **状态：RESERVED（占位 · 开放认领）** — 本仓已按平台协议规范建好行业接入四件套骨架，
> 等待具备本域资质的运营方认领并填充真实规则。

把「这个网站/服务要不要办证、办哪种」拆成可核验的属性，让 AI 只做路径提示，不做上线与许可结论。

## 这个域管什么

互联网信息服务与增值电信业务许可核验

ICP 备案与增值电信业务经营许可常被混淆，前者是备案、后者是许可，适用情形不同；数据本地化与内容合规是叠加义务。AI 能做的是把业务形态与许可状态摆清楚，许可权在电信主管部门。

## 域标识

| 项 | 值 |
|---|---|
| 域 ID | `tel`（全局唯一，一经分配不复用） |
| 域名称 | 电信 · ICP 与增值电信业务许可 |
| Profile 版本 | `domain/1.0` |
| 当前状态 | `RESERVED` |
| 占位时间 | 2026-09-12 |

## 属性清单

| 属性键 | 类型 | 说明 |
|---|---|---|
| `tel.service_category` | enum | 按电信业务分类目录划分的业务类别，决定适用备案还是许可 · 取值 information_service/value_added/basic/other |
| `tel.license_type` | enum | 非经营性备案 / 经营性许可 / 无需办理 · 取值 icp_filing/icp_license/none/not_required/undetermined |
| `tel.filing_status` | enum | 备案或许可当前状态，以电信主管部门公示为准 · 取值 filed/pending/cancelled/none/not_required |
| `tel.data_localization` | enum | 数据境内存储义务落实情况 · 取值 compliant/deviation/not_applicable |
| `tel.content_compliance` | enum | 内容合规与整改通知情况 · 取值 compliant/rectification_required/violation/unknown |

## 本域红线（不可逾越，机器可读）

1. 不得输出「可上线」「可运营」放行结论，以电信主管部门许可为唯一依据
2. 未取得相应许可不得给出可开展增值电信业务的表述
3. 不得建议以境外部署、域名跳转、挂靠他人资质等方式规避许可要求

> 红线在 `gate-map.json` 中均有对应阻断规则。平台校验器会检查「每条红线都有规则覆盖」，
> 缺失即校验失败——**制度与系统不允许不同步**。

## 行业接入四件套

| 文件 | 作用 |
|---|---|
| `domain.manifest.json` | 本域声明：属性清单、签发方要求、有效期、红线 |
| `gate-map.json` | 本域「什么动作要多少摩擦」：silent / warn / confirm / block / require-owner |
| `privacy.json` | 本域隐私声明：默认关闭、最小必要、可撤回、可删除 |
| `checker` | 本域核验器（MCP 工具，**只出示核验，不下判定**） |

## 核心原则

**平台只当擂台，不当货架。** 本域的核验器只回答「这条声明是否可核验、缺什么要件」，
不回答「这件事是否合规、该不该做」。判定权在本域的资质方、监管方与人。

**隐私是准入条件，不是整改事项。** 缺失 `privacy.json` 或任一必填字段不符，
符合性校验直接失败——不是警告，是拒绝接入。

## 参考依据

- 中华人民共和国电信条例
- 互联网信息服务管理办法
- 电信业务分类目录
- 电信业务经营许可管理办法
- 非经营性互联网信息服务备案管理办法

> 上列依据仅用于说明本域属性的来源与口径，不构成法律意见。具体适用以现行有效文本与主管部门解释为准。

## 认领方式

本域面向具备相应资质的机构开放。认领后请：

1. Fork 本仓，填注 `operator` 与 `checker_endpoint`
2. 按本域现行有效规则校准属性取值与红线表述
3. 跑平台侧校验器自测（五项判据全过方可提交）
4. 提 PR，附资质证明与规则依据

## 许可与署名

代码与配置按 MIT 许可使用。文档的知识版权归 SynomosAI 所有。

© 2026 SynomosAI. All rights reserved.
