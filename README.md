# fingerprint-kernel-assets

这是 NetLops 自建指纹内核的资产归档仓。

职责只做三件事：

- 记录每个内核版本的 release metadata
- 记录构建产物的校验和、来源 run、notarization 信息
- 给外部大文件分发留一个稳定索引

不建议把这些大文件直接提交进 git：

- `Chromium.app`
- `.dmg`
- `.zip`
- 其他大体积构建缓存

推荐做法：

1. 大文件放 GitHub Releases、对象存储或私有制品库
2. 这个仓库只保留 metadata、checksums、release notes、notarization 记录

## 当前关联仓库

- Build repo:
  - [NetLops/fingerprint-kernel-build](https://github.com/NetLops/fingerprint-kernel-build.git)
- Source fork:
  - [NetLops/Ant-Browser](https://github.com/NetLops/Ant-Browser)
- Assets repo:
  - [NetLops/fingerprint-kernel-assets](https://github.com/NetLops/fingerprint-kernel-assets.git)

## 推荐目录

```text
fingerprint-kernel-assets/
  releases/
    146.0.7680.177-fk.1/
      manifest.json
      release-metadata.json
      checksums/
        sha256sums.txt
      logs/
        summary.txt
      notarization/
        README.md
  staging/
```

## 使用方式

构建成功后，从 `fingerprint-kernel-build` 里执行：

```bash
python3 scripts/archive_to_assets_repo.py \
  --manifest manifests/current.json \
  --run-id 24451150534 \
  --assets-repo /Users/netlops/Documents/ai/github/fingerprint-kernel-assets \
  --commit
```

如果后面你们要做完全自动化，可以直接用：

```bash
python3 scripts/run_build.py \
  --manifest manifests/current.json \
  --install \
  --set-default \
  --replace-existing \
  --archive-assets \
  --assets-repo /Users/netlops/Documents/ai/github/fingerprint-kernel-assets \
  --archive-commit
```
