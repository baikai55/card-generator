# 银行卡算号器（Luhn Lab）

基于 Luhn 算法的银行卡号**验证**与**生成**工具，纯前端单文件，部署在 Cloudflare Worker（静态资源）。

## 功能

- **验证模式**：输入纯数字卡号，自动校验是否符合 Luhn 算法。
- **生成模式**：输入含字母或 `*` 的模板，枚举所有符合 Luhn 校验、且匹配模板的组合，按卡号升序分页展示。
  - 字母规则：相同字母对应相同数字（`aaa` → `111` 等）。
  - 星号规则：每个 `*` 独立随机/枚举。
- **生成测试**：从当前模板随机抽取一条有效号并自动校验（无模板时使用默认模板）。
- 模版筛选、每四位分组、单条/整页复制、明暗主题、`?input=` 预填。

所有计算均在浏览器本地完成。

## 本地开发

```bash
npm install
npm run dev        # 本地预览（wrangler dev）
```

## 部署到 Cloudflare

### 方式一：Wrangler CLI

```bash
npx wrangler login
npm run deploy
```

### 方式二：Cloudflare Workers Builds（Git 自动部署）

1. 把本仓库推送到 GitHub/GitLab。
2. Cloudflare Dashboard → Workers & Pages → 创建 Worker → 连接 Git 仓库。
3. 构建命令 `npx wrangler deploy`，根目录留空。
4. 保存后每次 push 自动部署。

## 目录结构

```
public/index.html   页面（单文件，含全部逻辑）
wrangler.jsonc       Worker 静态资源配置
package.json         脚本与 wrangler 依赖
```

## 说明

仅用于支付表单、接口校验逻辑等测试场景，请勿用于任何非法用途。
