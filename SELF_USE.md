# self-use 分支说明

本分支是个人自用定制分支，基于 `upstream/main`（superturtlee/anland）最新进度同步而来，
保留 main 的全部功能，并叠加以下个性化设置与修复。

## 与 main 分支的区别

| 功能 | main 分支 | self-use 分支 |
|---|---|---|
| Back 键默认行为 | 默认打开扩展按键栏（`bound_keycode` 默认 `-1`） | 默认绑定为「系统软键盘切换键」（`bound_keycode` 默认 `KEYCODE_BACK`），可在设置中改回 |
| 扩展按键栏默认键 | 默认布局 | 额外加入 `C` `V` `SHIFT` `BS` `Enter` 快捷键行 |
| 双指开合 / 三指及以上手势 | 作为触摸转发到桌面（缩放等） | **默认禁用**，手势被吞掉；可在 设置 → 触摸板 → 「禁用双指开合与多指手势」中开启转发（默认开启禁用） |
| 软键盘弹出时抬起桌面 | 默认开启（`keyboard_floating` 默认 `false`） | 默认关闭（`keyboard_floating` 默认 `true`），软键盘浮动不压缩桌面区域 |
| 触摸板模式默认 | 默认关闭（`touchpad_mode` 默认 `false`） | 默认开启（默认 `true`），屏幕触摸板直接可用 |
| 鼠标加速度默认值 | `1.0` | `1.5`（设置项「鼠标灵敏度」） |
| 小窗（freeform）模式键盘 | main 早期无修复 | 已合入 freeform 键盘修复：键盘位置随窗口缩放重定位、IME 可见性自管理标志，扩展按键栏随软键盘同显同隐 |
| 应用签名 | 每次云编译随机生成 debug keystore | 本地与云编译共用同一固定 keystore（GitHub Secret `ANLAND_KEYSTORE_BASE64`），APK 可直接覆盖安装无需卸载 |

## 构建产物

- 云编译：push 到 `self-use` 自动触发 GitHub Actions「Build APK and Daemon」，产物见 Actions 页面的
  `anland-v5.apk` 与 `anland-daemon`（Magisk 模块）。
- 本地编译：见 `~/Desktop/本地编译说明.md`（aarch64 容器方案）。

## 签名说明

- 本地 `~/.android/debug.keystore` 是唯一签名源（别名 `androiddebugkey`，密码 `android`），
  请妥善保管、勿删除。
- 云编译通过仓库 Secret `ANLAND_KEYSTORE_BASE64`（该 keystore 的 base64）还原同一文件，
  保证本地/云端签名一致，升级无需卸载重装。
