# Vercel Deploy Minimal Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** 以最小改动让当前前端项目可稳定部署到 Vercel，并避免刷新二级路由时出现 404。

**Architecture:** 保持现有 React + Vite 前端结构不变，仅新增 Vercel 的 SPA 回退配置。部署平台中的安装与构建命令在 Vercel 后台设置，不改动现有业务逻辑与页面代码。

**Tech Stack:** React 18, React Router, Vite, Vercel

---

### Task 1: 新增 Vercel 路由回退配置

**Files:**
- Create: `vercel.json`

**Step 1: 新增最小配置文件**

```json
{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
```

**Step 2: 检查配置是否仅影响前端路由**

确认当前项目没有依赖 Vercel Serverless API 的 `/api/*` 路径；本次重写规则仅用于前端 SPA 页面回退。

**Step 3: 验证构建能力**

Run: `pnpm vite build`
Expected: 成功生成 `dist` 目录

**Step 4: 记录部署后台配置**

- Root Directory: `SIFF-FPmatch-main`
- Install Command: `pnpm install`
- Build Command: `pnpm vite build`
- Output Directory: `dist`

**Step 5: 提交**

```bash
git add vercel.json docs/plans/2026-05-30-vercel-deploy-minimal.md
git commit -m "chore: add minimal vercel deploy config"
```
