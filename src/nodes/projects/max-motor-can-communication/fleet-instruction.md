1. 基础指令

|命令	|构建|	烧录|	看日志|
|---|---|---|---|
|polyfw build|	是|	否|	否|
|polyfw flash|	否|	是|	否|
|polyfw run	|否|	是|	是|
|polyfw attach|	否	|否|	是（连接正在运行的程序）|

```bash
polyfw select                     # 交互选择要开发的板件，保存到 .polyfw-state/
polyfw select sentry-chassis --release

polyfw build                      # 构建已选固件
polyfw build sentry-chassis --dev # 临时指定固件和 profile
polyfw build --all-firmwares --release

polyfw flash                      # 烧录已有 ELF（不会自动 build）
polyfw run                        # 烧录 + 复位 + 读 RTT/defmt 日志
polyfw attach                     # 只连正在运行的程序读日志
polyfw reset
polyfw probes  

```


2. 检查与测试

```bash
polyfw fmt                 # 格式化（会改文件）
polyfw lint                # MCU + 主机 Clippy，警告即错误
polyfw test                # 主机测试（--target host-tuple）
polyfw verify              # fmt 检查 + Clippy + 测试

just files                 # 文档/文件/架构图检查
just ci                    # 整个业务 workspace：检查 + 依赖策略 + 全部 release 镜像
```


3. 完整项目流程演示

```bash
# 1. 先读硬件前提：接线、CAN3 必须连云台板、DR16 插云台板等
open robots/sentry/chassis-board/README.md

# 2. 选择并构建
polyfw select sentry-chassis --release
polyfw build

# 3. 接好探针和 24V 电源（只靠探针供电 CAN 收发器带不动电机）
polyfw probes
polyfw run        # 烧录并看 RTT 日志

# 4. 按 README 做零点/IMU 方向检查后，再让机器人动
```

