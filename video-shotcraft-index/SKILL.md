---
name: video-shotcraft-index
description: 根据作者提供的网站、目录、仓库或模板页链接建立或更新一个或多个在线视频模板库的索引，供 video-shotcraft-storyboard 跨库选镜和准确定位模板。
---

# 在线视频模板库索引

接受一个或多个链接。逐个打开，识别目录、分页、筛选、搜索、卡片详情、嵌入样片和变体切换的实际访问方式。若作者只给了库名，先搜索并核实官方或作者指定的来源。登记各库的实际可访问范围，逐个核对动效变体。按照 [观察规范](references/template-index.md) 记录画面、用途、素材与搭配信息。分批保存进度，更新时处理新增、变更和失效链接。

在项目根目录或作者指定的共享位置输出两份 UTF-8 JSONL：

- video-template-libraries.jsonl，每行一个库。记录 library_id、name、entry_url、catalog_access、checked_at、coverage。catalog_access 写明从入口进入目录及枚举的方法，包括实际菜单、筛选、分页、搜索或仓库路径。coverage 记录范围与各核对状态数量。
- video-template-index.jsonl，每行一个变体。记录 library_id、card、variant、source_url、preview_url、checked_at、status、motion、tags、use_cases、avoid、required_assets、replaceable_elements、edit_in、edit_out、notes、access。无变体时用 null。motion 包含 start、action、end、pace。标签、用途、避用场景、素材、可替换元素和衔接建议用字符串数组。

模板访问记录 access 包含：

- entry_url 和 steps。写可直接打开的入口，以及从该入口定位准确模板和变体的有序步骤，包含界面原文、搜索词、卡片标题、变体选择以及如何播放。可用深链时也保留实测可用的回退路径。
- identity_check。写到达后可核对的准确标题、变体标签或样片特征。标题重名时加目录位置或其他可验证的标识。
- implementation_url、implementation_ref 和 implementation_path。记录已核对的源文件、下载页或编辑器入口。仓库模板尽可能记录版本或提交、相对路径以及运行该模板所需入口。字段不适用或无法核实时用 null，并在 notes 中解释。
- requirements。记录实测的登录、权限、付费、浏览器交互或其他访问条件。按库需要增加站点特有定位字段时，保留上述通用字段和可读步骤。

尽可能从记录的入口独立重走步骤，确认落到同一变体。status 取 preview_verified、text_only 或 pending，实际看过动效才标 preview_verified。校验两份文件均逐行可解析，library_id 可关联，库内卡片和变体唯一。比较已枚举目录与覆盖范围，交付路径和无法核对的部分。
