# 更新日志

## 1.0.1 (2026-11-13)

兼容性修复版本，无接口行为变更，升级无需改动调用方代码。

### PHP 8.4 / 8.5 兼容修复

- `QiniuAdapter::getUploadToken()`：`?string $key`、`?array $policy`、`?string $strictPolice` 由隐式可空改为显式可空，消除 PHP 8.4+ 的 `Implicitly marking parameter as nullable is deprecated`。
- `QiniuAdapter::verifyCallback()`：`?string $contentType`、`?string $originAuthorization`、`?string $url`、`?string $body` 同样改为显式可空。
- 合计 7 处隐式可空参数，其余扫描项（`${}` 插值、已废弃函数、`E_STRICT`、非规范类型强转、动态属性等）均为 0 命中；未引入 PHP 8.1+ 语法，`>=8.0` 可用。

### 元数据

- 新增 `require.php: >=8.0`：源码使用构造器属性提升、联合类型等 PHP 8.0 特性。
- 补充 `type`、`keywords`、`description`。
- 移除 `extra.hooks` 与 `cghooks` 相关脚本：这些脚本依赖未声明的 `cghooks`，在包仓库内执行 `composer install` 会直接失败。
- 版本由 Git 标签 `v1.0.1` 决定。
- 新增 `topthink/framework: ^6.1 || ^8.0` 依赖声明；补充 `LICENSE`（MIT 全文，与 `license` 字段一致）。

### 已知问题（未在本次修改）

- `readStream()` 声明返回 `string`，实际返回资源句柄，PHP 8.x 下调用会抛 `TypeError`。属既有类型声明缺陷，改动会影响对外方法签名，待确认后单独修复。
