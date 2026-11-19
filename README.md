# OpenWRT-CI-Lite
云编译OpenWRT固件（精简版：仅编译 ROCKCHIP / X86 / R68S 三个配置）。

编译核心及优化脚本来源：VIKINGYFY - https://github.com/VIKINGYFY/OpenWRT-CI

源码：https://github.com/immortalwrt/immortalwrt.git（master）

# 固件简要说明

固件每天早上5点自动编译（Auto-Clean 完成后触发 OWRT-ALL）。

固件信息里的时间为编译开始的时间，方便核对上游源码提交时间。

# 编译优化

- 按 源码/分支/平台 分代缓存（ccache + host/tool 工具链），上游提交变化时自动回退到同平台最近缓存，并在成功后轮换旧缓存
- 使用 runner 自带 Go / Rust 引导，免去源码编译宿主 Go、Rust
- 关闭宿主 Python PGO，BPF 工具链统一使用宿主 LLVM
- 精简构建依赖，每次编译输出耗时/ccache 报告（Artifacts）

# 需要的 Secrets

GH_TOKEN（读取私有仓库 qqsir-dev/config，Contents: Read）、PPPOE_X86_USER、PPPOE_X86_PASS、PPPOE_R68_USER、PPPOE_R68_PASS

# 目录简要说明

.github/workflows——CI配置　.github/scripts——编译优化脚本　Scripts——自定义脚本　Config——自定义配置
