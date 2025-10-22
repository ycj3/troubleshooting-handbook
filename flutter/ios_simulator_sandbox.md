在 iOS 模拟器中运行的 App，其**沙盒目录（sandbox）** 包含了 App 可读写的 `Documents`、`Library`、`tmp` 等目录。这个路径因设备和 App 而异，但格式是固定的。

## iOS 模拟器中沙盒目录路径

```
~/Library/Developer/CoreSimulator/Devices/<Device UDID>/data/Containers/Data/Application/<App UUID>/
```

里面包含：

- `Documents/`
- `Library/`
- `tmp/`

## 如何查找当前 Flutter App 的沙盒路径

你可以按照下面的步骤操作：

### 步骤 1：找出当前正在运行的模拟器设备 UDID

```bash
xcrun simctl list devices | grep Booted
```

输出示例：

```
iPhone 15 (BE9713EF-13C1-4B22-A6E7-123456789ABC) (Booted)
```

其中 `BE9713EF-13C1-4B22-A6E7-123456789ABC` 就是 Device UDID。

### 步骤 2：进入 Data 目录下的 App 数据容器路径

```bash
cd ~/Library/Developer/CoreSimulator/Devices/<Device UDID>/data/Containers/Data/Application/
```

比如：

```bash
cd ~/Library/Developer/CoreSimulator/Devices/BE9713EF-13C1-4B22-A6E7-123456789ABC/data/Containers/Data/Application/
```

### 步骤 3：找到你 App 的沙盒目录

这个目录下有多个 UUID 命名的文件夹，每一个都是一个 App 的沙盒。你可以用以下命令找出你的 Flutter App 的那个：

```bash
grep -r "your_bundle_identifier"
```

## 日志追踪

用 `tail -f ` 实时监视日志文件

```bash
tail -f "your_logfile_path"
```
