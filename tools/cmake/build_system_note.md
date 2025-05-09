# 构建系统备注

本文主要用于记录构建系统所需变量与 CMake 定义的变量的位置。

## 所需环境变量

以下变量可在 esp-idf 中通过 `. ./export.sh` 查看。

```bash
export IDF_PATH="/home/user_name/esp-idf-v5.4"
# xf_platform 中暂未需要
# export ESP_IDF_VERSION="5.4"
# xf_platform 中暂未需要
# export IDF_PYTHON_ENV_PATH="/home/user_name/.espressif/python_env/idf5.4_py3.10_env"
# xf_platform 中暂未需要
# export OPENOCD_SCRIPTS="/home/user_name/.espressif/tools/openocd-esp32/v0.12.0-esp32-20241016/openocd-esp32/share/openocd/scripts"
# xf_platform 中不需要
# export ESP_ROM_ELF_DIR="/home/user_name/.espressif/tools/esp-rom-elfs/20241011/"
# xf_platform 中暂未需要
# export PATH="/home/user_name/esp-idf-v5.4/components/espcoredump:/home/user_name/esp-idf-v5.4/components/partition_table:/home/user_name/esp-idf-v5.4/components/app_update:/home/mao/.espressif/tools/xtensa-esp-elf-gdb/14.2_20240403/xtensa-esp-elf-gdb/bin:/home/mao/.espressif/tools/riscv32-esp-elf-gdb/14.2_20240403/riscv32-esp-elf-gdb/bin:/home/mao/.espressif/tools/xtensa-esp-elf/esp-14.2.0_20241119/xtensa-esp-elf/bin:/home/mao/.espressif/tools/riscv32-esp-elf/esp-14.2.0_20241119/riscv32-esp-elf/bin:/home/mao/.espressif/tools/esp32ulp-elf/2.38_20240113/esp32ulp-elf/bin:/home/mao/.espressif/tools/openocd-esp32/v0.12.0-esp32-20241016/openocd-esp32/bin:/home/mao/.espressif/python_env/idf5.4_py3.10_env/bin:/home/user_name/esp-idf-v5.4/tools:$PATH"
# xf_platform 中暂未需要
# export IDF_DEACTIVATE_FILE_PATH="/tmp/tmpb4530s_yidf_51501"
# xf_platform 中暂未需要
# export IDF_TOOLS_INSTALL_CMD="/home/user_name/esp-idf-v5.4/install.sh"
# xf_platform 中暂未需要
# export IDF_TOOLS_EXPORT_CMD="/home/user_name/esp-idf-v5.4/export.sh"
```

## 常用 CMake 变量

| 变量名       | 类型/值 | 作用             | 可用范围        | 位置                    | 备注                     |
| ------------ | ------- | ---------------- | --------------- | ----------------------- | ------------------------ |
| ESP_PLATFORM | 1       | 标识 esp-idf     | 组件 CMakeLists | tools/cmake/build.cmake |                          |
| XF_PLATFORM  | 1       | 标识 xf_platform | 组件 CMakeLists | tools/cmake/build.cmake | 与 ESP_PLATFORM 同时存在 |
|              |         |                  |                 |                         |                          |
