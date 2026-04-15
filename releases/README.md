# Releases Layout

每个版本一个目录：

```text
releases/<kernel-version>/
  manifest.json
  release-metadata.json
  checksums/sha256sums.txt
  logs/summary.txt
  notarization/README.md
```

说明：

- `manifest.json`：构建时使用的 kernel manifest
- `release-metadata.json`：版本、来源 run、发现到的 archive、生成时间
- `checksums/sha256sums.txt`：归档文件校验和
- `logs/summary.txt`：关键日志摘要，不放超大原始 build log
- `notarization/README.md`：当前版本的签名、公证记录说明
