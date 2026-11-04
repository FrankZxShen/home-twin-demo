# 05 相关工作

[返回首页](../README.md) · [上一章：工具与实现](04-tools.md) · [下一章：验证计划](06-evaluation-plan.md)

本页组织已有阅读记录及前一轮核对的原始来源，说明借鉴与比较关系。完整复现配置和组合机制的查新仍需补齐。

## 5.1 最相关的论文

| 论文 | 与本项目相关的内容 | 在本项目中的用途 |
| --- | --- | --- |
| [UrbanVerse: Scaling Urban Simulation by Watching City-Tour Videos](https://arxiv.org/html/2510.15018) | 从城市导览视频提取布局，检索资产，生成仿真场景 | 借用建场景流程；检查改到室内需要哪些组件 |
| [EvolvingNav / Beyond the Remembered World](https://arxiv.org/html/2609.39166v4) | 根据历史与新观测更新物体位置判断；处理有限可见度下的未检出证据 | 找物与记忆更新的主要相关工作；核对其观察与证据更新机制 |
| [Object- and Task-Aware Active Perception](https://arxiv.org/html/2610.29964v1) | 移动机械臂在导航中主动观察不确定或安全相关区域 | 主动观察的重要对照；比较移动观察站位与调整相机视角 |
| [3DGS-CD](https://arxiv.org/abs/2411.03706) | 利用新视角渲染与图像比较检测物体重排 | 核对“渲染参照与实拍比较”的已有机制 |
| [NavPatch](https://arxiv.org/html/2609.14543v1) | 根据视觉与几何证据修改物体相关导航代价区域 | 导航约束更新的相关工作；比较证据如何影响要求状态 |
| [KnowNo / Robots That Ask For Help](https://proceedings.mlr.press/v229/ren23a.html) | 对规划不确定性进行处理，在需要时向人求助 | 询问主人的决策参考 |
| [Automated Creation of Digital Cousins for Robust Policy Learning](https://arxiv.org/abs/2410.07408) | 使用几何和功能相近的场景训练机器人策略 | 相似资产与近似场景的建模参考 |

## 5.2 Jev 的来源

Jev 是模型与 API 产品，本页按官方技术来源记录：

- [Primitives 文档](https://docs.typesafe.ai/primitives)：带类型的小问题、Choice 选项概率，以及由代码组合判断结果的用法。
- [2026-10-14 图像功能公告](https://typesafe.ai/blog/jev-1-14)：实验性图像输入和相关能力说明。

本项目借鉴它的判断接口，也可以评估它作为模型的效果。当前没有 Jev 在本项目家庭数据上的测量结果。

## 5.3 需要继续补读的方向

| 方向 | 已有方案中的候选 | 要查清的问题 |
| --- | --- | --- |
| 遮挡与下一观察视角 | OA-NBV、IVAM-Nav | 是否已考虑地图或孪生误差，以及观察后怎样确认目标状态 |
| 从真实住宅构造仿真 | Phone2Proc、MetaScenes、EmbodiedSplat | 建模输入、可交互部件、几何误差和使用成本 |
| 物体持久性与变化 | POCD、持久性滤波、Perpetua | 未检出与遮挡如何进入状态估计 |
| 规则与任务完成 | NORM-Nav、Done, But Not Sure | 规则如何绑定对象，完成判定需要什么证据 |

这些条目沿用原方案的补读方向，尚未据此形成完整方法比较。

## 5.4 需要 co-author 判断的新意边界

1. 孪生同时用于出发前选站位和到达后判断，是否形成一个值得单独验证的机制？
2. 四类判断、深度参照与概率校准的组合，相比已有变化检测和可见度更新增加了什么能力？
3. 按实测建模误差及检索候选生成扰动，和已有稳健下一视角选择有什么重合？
4. 长期要求跟着具体物体移动，应放在核心问题设定还是扩展应用中？

原方案中的简化策略对照需要与论文完整方法区分。采用固定视角或超时撤销策略时，应按实际实现命名；只有复现并核对了完整配置，才报告与原方法的比较。
