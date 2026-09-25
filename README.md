# Copy — UE5 数据驱动的「材料配比」小游戏

> 用 UE5 做的一个小游戏原型:按配方挑选建筑材料并观察结果,支持「改造前 / 改造后」两套场景对比。
> 全部逻辑用蓝图 + 数据表实现,新增材料只需要加一行数据。

## 简介

| | |
|---|---|
| **项目类型** | 数据驱动的小游戏原型(材料配比 / 建筑改造) |
| **引擎版本** | Unreal Engine 5.3 |
| **实现方式** | 纯蓝图(无 C++ 源码) |
| **用到的引擎系统** | DataTable + Struct + Enum(数据驱动)、UMG(条形表 / 材料表 / 提示)、关卡切换 |
| **仓库规模** | 蓝图与资产 36 个 |
| **入口关卡** | `/Game/after`(改造后场景),`/Game/before` 为改造前场景 |

## 功能流程

```
进入场景(改造前) → 挑选材料 / 配方 → 提交 → 切换到改造后场景 → 展示结果与提示
```

## 实现要点

- **数据表驱动玩法**:材料用 `Enum(类型)+ Struct(名称/配比/效果)+ DataTable(具体数值)` 三层定义,界面与玩法逻辑都从数据表读 —— 新增材料只加一行数据,不碰蓝图。
- **before / after 双场景**:同一关卡的两种状态,玩家操作后切换到「改造后」场景做对比,改造结果直接可见。
- **多层 UI 反馈**:材料条形表、目标提示、进度条与分级警告提示(材料不足 / 配比错误等在数据表里配好),反馈分层给出而不是一句话糊过去。

## 目录结构

```
Copy.uproject
Config/                   项目配置
Content/
  Blueprint/              GM_GameMode、before / after 关卡蓝图
  MaterialData/           E_MaterialType(枚举)+ S_MaterialData(结构体)+ DT_MaterialData(数据表)
  UI/                     条形表、材料表、目标与警告提示
  image/                  材料与界面素材
  before.umap after.umap  改造前 / 改造后关卡
```

## 如何打开

1. 安装 **Unreal Engine 5.3**。
2. `git clone` 本仓库,双击 `Copy.uproject`(纯蓝图工程,不需要编译)。
3. 若关卡里提示缺失模板资源,用 UE 新建一个 **Third Person 模板** 工程,把它的 `Content/StarterContent`
   与 `Content/Characters` 拷进本项目 `Content/` 下。
4. 默认关卡为 `/Game/after`。

## 说明

- 仓库只包含本人产出的蓝图、数据表、UI 与素材;UE 官方模板资源未包含(见"如何打开"第 3 步)。
