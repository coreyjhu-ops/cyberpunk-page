# 人生足迹项目技术文档（0.1 -> 1.1）

## 1. 文档范围

本文档仅覆盖“人生足迹”产品线的研发过程，不包含该仓库在此前阶段的其他页面形态。

覆盖版本区间：`0.1` 到 `1.1`。

---

## 2. 版本规则

1. 大版本 `0.x`：快速迭代阶段（核心能力逐步闭环）。
2. 大版本 `1.x`：核心闭环完成后的功能扩展阶段。

当前版本：`1.1`。

---

## 3. 迭代总表（0.1 -> 1.1）

| 版本 | 提交 Commit | 日期 | 版本主题 | 结果摘要 |
|---|---|---|---|---|
| 0.1 | `0950c27` | 2026-03-02 | 足迹地图初版 | 地图、打点、历史、轨迹与时间筛选 |
| 0.2 | `813b59e` | 2026-03-02 | 云同步与撤回 | 接入 Supabase，实现跨设备同步与撤回 |
| 0.3 | `fbbeed5` | 2026-03-02 | 登录与用户隔离 | 引入账号体系，按用户读取自己的记录 |
| 0.4 | `64f407a` | 2026-03-02 | 交互修复与布局重构 | 修复注册反馈，筛选区移至左侧且不遮挡地图 |
| 0.5 | `6a1877d` | 2026-03-02 | 注册弹窗与地点名展示 | 注册独立弹窗（双密码确认），历史显示地点名 |
| 1.0 | `b4a6fe4` | 2026-03-02 | 地点名持久化与轨迹方向 | 地点名可编辑并持久化，轨迹增加方向箭头 |
| 1.1 | `（本次实现）` | 2026-03-02 | 我的旅程体系 | 新增旅程创建/管理/单旅程展示，支持旅程内地点增删 |

---

## 4. 各版本详细说明（新增功能 + 解决问题）

### 4.1 版本 0.1

新增功能：

1. Leaflet 地图加载与基础视图。
2. “记录当前位置”打点。
3. 历史记录面板（时间 + 经纬度）。
4. 两种展示模式：全部地点 / 轨迹连线。
5. 时间区间筛选。

解决问题：

1. 从普通展示页转为可交互的足迹记录应用。
2. 建立“采集 -> 展示 -> 回看”的基础闭环。

---

### 4.2 版本 0.2

新增功能：

1. 接入 Supabase 云数据库。
2. 支持云端读取/写入位置记录。
3. 新增“撤回上一次记录”按钮。

解决问题：

1. 解决本地存储导致的“电脑记录、手机不可见”。
2. 实现跨设备共享同一份记录数据。

---

### 4.3 版本 0.3

新增功能：

1. 接入 Supabase Auth（注册/登录/退出）。
2. 记录按 `user_id` 绑定登录用户。
3. 页面只读取当前登录用户的数据。

解决问题：

1. 解决多人使用同一项目时数据混杂问题。
2. 实现用户级数据隔离与归属。

---

### 4.4 版本 0.4

新增功能：

1. 注册/登录反馈文案强化。
2. 布局升级为“左侧控制 + 中间地图 + 右侧历史”。
3. 删除冗余说明块，主流程更聚焦。

解决问题：

1. 解决注册“无反馈感”的交互问题。
2. 解决筛选控件遮挡地图的问题。

---

### 4.5 版本 0.5

新增功能：

1. 注册流程改为独立弹窗。
2. 注册增加“二次密码确认”。
3. 历史记录显示地点名（不再仅经纬度）。
4. 地图弹窗同步显示地点名。

解决问题：

1. 解决登录与注册混在一起导致流程不清。
2. 解决仅经纬度难以识别真实地点。

---

### 4.6 版本 1.0

新增功能：

1. `place_name` 持久化写入数据库。
2. 用户可手动修改地点名并回写数据库。
3. 轨迹模式连线上增加方向箭头。
4. 缺列/缺策略场景提供前端可读错误提示。

解决问题：

1. 解决地点名刷新后丢失的问题。
2. 解决自动地点名不准确时无法纠正的问题。
3. 解决轨迹“仅连线不显方向”的问题。

---

### 4.7 版本 1.1

新增功能：

1. 新增“我的旅程”模块：
   1. 添加新的旅程按钮
   2. 我的旅程管理按钮
2. 新增“创建/加点”旅程编辑弹窗：
   1. 创建旅程时输入旅程名
   2. 在弹窗中按时间筛选地点
   3. 选择地点加入旅程
3. 新增“我的旅程”管理弹窗：
   1. 显示该旅程（地图+历史切换到该旅程）
   2. 添加地点到旅程
   3. 重命名旅程
   4. 删除旅程
   5. 从旅程移除地点
4. 新增旅程视图横幅：显示当前旅程并支持退出旅程视图。
5. 旅程轨迹按 `visited_at` 升序连线，并保留方向箭头。
6. 加入旅程表缺失/RLS缺失的错误提示。

解决问题：

1. 解决全量轨迹混杂、无法按“某次旅程”查看的问题。
2. 解决地点无法按旅程组织管理的问题。
3. 解决旅程后续维护困难（无法增删点/重命名/删除）的问题。

---

## 5. 当前 1.1 能力清单

1. 登录/注册/退出（Supabase Auth）。
2. 地图打点、历史记录、全局时间筛选。
3. 全部地点模式与轨迹模式。
4. 轨迹方向箭头。
5. 撤回最后一次记录。
6. 自动地点名解析 + 数据库存储。
7. 用户自定义修改地点名并持久化。
8. 我的旅程：创建、加点、显示、重命名、删除、移除地点。
9. 旅程视图：地图与历史同步切换为单旅程数据。
10. 手机/桌面响应式布局。

---

## 6. 1.1 对应数据库要求（Supabase）

### 6.1 既有要求（1.0）

```sql
alter table public.travel_points
add column if not exists place_name text;

create policy "Users can update own points"
on public.travel_points
for update
to authenticated
using ((select auth.uid()) = user_id)
with check ((select auth.uid()) = user_id);
```

### 6.2 新增要求（1.1）

```sql
create table if not exists public.travel_journeys (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  name text not null,
  created_at timestamptz not null default now(),
  updated_at timestamptz not null default now()
);

create table if not exists public.travel_journey_points (
  id uuid primary key default gen_random_uuid(),
  journey_id uuid not null references public.travel_journeys(id) on delete cascade,
  point_id uuid not null references public.travel_points(id) on delete cascade,
  user_id uuid not null references auth.users(id) on delete cascade,
  created_at timestamptz not null default now(),
  unique (journey_id, point_id)
);

create index if not exists idx_travel_journeys_user_created
on public.travel_journeys (user_id, created_at desc);

create index if not exists idx_travel_journey_points_journey
on public.travel_journey_points (journey_id, created_at);

create index if not exists idx_travel_journey_points_user
on public.travel_journey_points (user_id, created_at desc);

alter table public.travel_journeys enable row level security;
alter table public.travel_journey_points enable row level security;

create policy "Users can read own journeys"
on public.travel_journeys
for select to authenticated
using ((select auth.uid()) = user_id);

create policy "Users can insert own journeys"
on public.travel_journeys
for insert to authenticated
with check ((select auth.uid()) = user_id);

create policy "Users can update own journeys"
on public.travel_journeys
for update to authenticated
using ((select auth.uid()) = user_id)
with check ((select auth.uid()) = user_id);

create policy "Users can delete own journeys"
on public.travel_journeys
for delete to authenticated
using ((select auth.uid()) = user_id);

create policy "Users can read own journey points"
on public.travel_journey_points
for select to authenticated
using ((select auth.uid()) = user_id);

create policy "Users can insert own journey points"
on public.travel_journey_points
for insert to authenticated
with check (
  (select auth.uid()) = user_id
  and exists (
    select 1 from public.travel_journeys j
    where j.id = journey_id and j.user_id = (select auth.uid())
  )
  and exists (
    select 1 from public.travel_points p
    where p.id = point_id and p.user_id = (select auth.uid())
  )
);

create policy "Users can delete own journey points"
on public.travel_journey_points
for delete to authenticated
using ((select auth.uid()) = user_id);
```

---

## 7. 结论

从 `0.1` 到 `1.1`，项目已从“位置记录工具”升级为“可登录、可同步、可追踪、可编辑语义地点、可按旅程组织和复盘”的完整个人足迹系统。
