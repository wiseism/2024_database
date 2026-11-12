# 修复 CMake workflow：sync-gitlab/sync-gitee job 失败

## 失败信息
- Run 42817008254（CMake）：build ✅，但 sync-gitlab / sync-gitee job failure。

## 原因分析
- workflow 中的镜像同步 job 需要额外的凭据/远端配置，在账户当前状态下不可用；
  build 本身无问题。

## 修复内容
- 移除 sync-gitlab/sync-gitee job，保留 build/test 主流程。

## 验证记录
| Run | 结果 |
|---|---|
| 43219537433 (workflow_dispatch) | ✅ success |
| 42817008254 (修复前) | failure — sync job 失败 |
