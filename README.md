# ChunkerPatch

为 [Chunker](https://github.com/HiveGamesOSS/Chunker) 添加网易版 Minecraft 支持的补丁项目。

## 功能

本补丁在官方 Chunker 基础上添加以下功能：

- **preserveUnknownEntities** - 保留未知实体的原始 NBT 数据
- **preserveUnknownBlockEntities** - 保留未知方块实体的原始 NBT 数据
- **NetEase ModBlock 支持** - 将非原版方块实体转换为网易版 `ModBlock` 格式

## 版本信息

| 组件 | 版本 |
|------|------|
| Chunker 基础版本 | 1.14.0 |
| 支持的 Java 版 | 1.8.8 - 1.21.11 |
| 支持的 Bedrock 版 | 1.12.0 - 1.21.130 |

## 目录结构

```
ChunkerPatch/
├── Chunker/                              # Chunker 官方仓库 (Git submodule)
├── 0001-Implement-netease-support.patch  # 网易版支持补丁
└── README.md
```

## 使用方法

### 1. 初始化子模块

```bash
git submodule update --init --recursive
```

### 2. 更新到最新版本

```bash
cd Chunker
git fetch origin
git checkout origin/main --detach
```

### 3. 应用补丁

```bash
git apply ../0001-Implement-netease-support.patch
```

### 4. 构建并安装到本地 Maven

```bash
chmod +x ./gradlew
./gradlew :cli:publishToMavenLocal
```

## 补丁修改的文件

| 文件 | 修改内容 |
|------|----------|
| `WorldConverter.java` | 添加 `preserveUnknownEntities/BlockEntities` 设置 |
| `Converter.java` | 添加接口方法 |
| `BedrockColumnWriter.java` | 添加 NetEase ModBlock 写入逻辑 |
| `*EntityResolver.java` | 修改未知实体保留逻辑 |
| `*BlockEntityResolver.java` | 修改未知方块实体保留逻辑 |
| `CLI.java` | 添加 CLI 参数支持 |
| `ConvertRequest.java` | 添加请求参数 |
| `app/*` | 添加 UI 配置选项 |

## 依赖此项目

在 Gradle 中使用：

```gradle
repositories {
    mavenLocal()
}

dependencies {
    implementation 'com.hivemc.chunker:cli:1.14.0'
}
```

## 相关项目

- [ChunkerFabric](../ChunkerFabric) - Fabric 服务端 Mod 封装
- [ChunkerSpigot](../ChunkerSpigot) - Spigot 服务端插件封装
