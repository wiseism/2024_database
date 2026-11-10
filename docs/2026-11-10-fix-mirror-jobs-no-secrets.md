# 2026-11-10 build.yml mirror 同步 job 失败修复

## 现象

GitHub Actions `CMake` workflow 中 `build` job 成功，但 `sync-gitee` / `sync-gitlab` 两个 job 失败：

```
Host key verification failed.
fatal: Could not read from remote repository.
```

## 根因

- sync job 使用 `yesolutions/mirror-action` 通过 SSH 同步，需要仓库 secrets `GITEE_RSA_PRIVATE_KEY` 等私有凭据；
- 经 API 查询，仓库 `2024_database` 中**没有任何配置的 secrets**（`secrets: []`），远程为课程方镜像（git@gitee.com:thu-db/huadb.git、git@git.tsinghua.edu.cn），普通 GitHub runner 亦无写入权限。

## 修复

从 `.github/workflows/build.yml` 中删除 `sync-gitee` / `sync-gitlab` 两个 job，保留可正常运行的 `build` job。
