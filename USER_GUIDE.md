# VaultGuard / 密码保险箱
## 软件介绍与官方使用说明书 | Software Introduction & User Manual
*(Package: com.freytagnan.pwdmanager_local)*

---

# 📖 中文版说明书 (Chinese Edition)

## 一、 软件定位与核心理念

**VaultGuard（密码保险箱 - 离线版）** 是一款专为极致数据安全与隐私设计的**纯本地单机高安全密码与两步验证（2FA/TOTP）管理器**。

在云端数据泄露事件与第三方静默数据收集日益频繁的今天，VaultGuard 坚持**“无网络权限（Zero Network Permission）”**与**“本地认证加密（AEAD）”**架构：
- **物理切断网络权限**：应用在操作系统底层清单中彻底剔除并阻断了 `android.permission.INTERNET` 与 `android.permission.ACCESS_NETWORK_STATE` 网络权限，无任何后台服务器、无远程 API、无分析追踪代码。
- **本地硬件与认证加密**：主加密密钥由用户自主掌握的主密码通过 **Argon2id** 算法派生，并在设备安全硬件芯片（Android Keystore / TEE / StrongBox）隔离保护下，对所有数据采用 **XChaCha20-Poly1305**（默认 256 位认证加密，配合 24 字节安全随机扩展 Nonce）或 **AES-256-GCM** 工业级强算法进行本地认证加密。
- **纯本地零外泄**：所有数据均只保留在您当前设备的本地私有加密数据库中，开发者无法访问您的主密码或保险箱数据，绝无任何主动外部通信通道。
- **目标受众声明**：本应用面向具备数字资产管理能力、能够独立妥善保管主密码与灾备责任的**成年用户（18 岁及以上）**设计。

---

## 二、 核心功能特性

1. **多维凭据类型支持**：
   - **常规账号密码**：支持标题、登录用户名/邮箱、安全密码以及专属的 3 项自定义备注（**备注1**、**备注2**、**备注3**）。
   - **API 密钥与服务 Token**：专为开发者与极客设计，便捷管理 OpenAI、AWS、GitHub、云服务器等各种生产 API 密钥与端点。
   - **密保助记词（Mnemonic Phrases）**：安全存储区块链钱包、加密资产的 12/24 位英文助记词，支持自动切词分块卡片展示。
   - **两步动态验证码（TOTP/2FA）**：基于 RFC 6238 标准的 30 秒动态令牌发生器，支持毫秒级时间进度圆环、一键复制验证码、相机直接扫码与相册图片解析导入。
2. **高熵密码生成器**：
   - 内置伪随机高熵生成引擎，支持大写字母、小写字母、数字及特殊符号组合。
   - 支持自定义密码长度（最长 64 位），并提供实时比特熵（Entropy bits）与安全评级评估。
3. **Android 系统级自动填充（Autofill Service）**：
   - 无缝集成 Android 原生自动填充框架，在浏览器或常用 App 登录时，经生物识别或主密码授权后秒级填入凭据。严格校验包名与 Web 域名等价关系，具备钓鱼防护机制。
4. **灵活的双轨备份与灾备**：
   - **加密数据库备份**：导出受独立强密码与认证加密保护的 `.sqlite` 加密备份文件，支持原子完整性校验与跨设备安全恢复。
   - **通用 CSV 导入导出**：支持与 Chrome、Bitwarden、KeePass 等工具兼容的 CSV 数据互导，内置 CSV 公式注入（Formula Injection）与超大文件 DoS 防护。
5. **硬件级生物识别快速解锁**：
   - 兼容设备指纹与面容解锁（BiometricPrompt），并在 StrongBox / TEE 硬件级别隔离主密钥。生物识别失效时严格回退为主密码，绝无绕过后门。

---

## 三、 详细使用操作指南

### 1. 首次初始化保险箱
1. 下载并安装安装包后打开应用，系统将展示“开启您的加密空间”初始化界面。
2. **设置主密码**：主密码是保护您本地所有资产的唯一钥匙。
   - 必须满足安全合规性要求：**长度至少 10 位**，必须同时包含**大写字母、小写字母、数字以及特殊符号**，且不得包含空格。
3. **再次确认主密码**：确保两次输入的密码完全一致。
4. **勾选同意条款**：阅读《用户服务协议》与《隐私政策》后勾选同意。
5. 点击 **“生成加密数据库”**，系统将利用 Argon2id 派生数据加密密钥（DEK）并建立本地强加密 SQLite 数据库。
6. **首次进入安全与防丢须知弹窗**：
   - **数据加密范围说明**：密码条目中仅【标题】保持明文用于本地毫秒级索引与全局快速检索；而【账号】、【密码/口令】、【双重验证 (2FA)】以及【备注1/2/3】等所有敏感核心信息，均在底层经过硬件级算法强加密存储，绝无明文泄露风险。
   - **卸载防丢警告**：由于本软件为 100% 纯本地离线单机应用，不设任何云端服务器，且应用主动配置了 `android:allowBackup="false"` 禁用了系统云端备份。卸载应用或清除系统应用数据将彻底删除本地私有数据库。如需更换设备、刷机或卸载应用，请务必提前在【我的】页面导出 `.sqlite` 加密备份文件保存！
> **⚠️ 核心警示**：由于本应用采用纯本地单机架构，没有云端服务器，开发者亦无法访问您的主密码，**主密码一旦遗失将永久无法找回或重置！请务必牢记您的主密码，建议将其抄写在纸质离线介质上安全存放。**

### 2. 日常解锁与生物识别
- **密码解锁**：输入初始化时设置的主密码，点击“解锁保险箱”。
- **生物识别解锁**：在应用设置中开启“生物识别快速解锁”后，每次打开应用可直接通过指纹或面容识别一秒解锁。
- **锁定与防窥保护**：在锁定状态和凭据查看页，系统强制启用 `FLAG_SECURE` 防截屏与录屏，并在多任务列表中隐藏界面缩略图。

### 3. 添加与管理凭据
1. 在主界面右下角点击悬浮添加按钮 **“+”** 打开新增弹窗。
2. **选择凭据类型**：常规存储密码、API 密钥、密保助记词、或两步动态验证码 (TOTP)。
3. **输入字段**：
   - **标题**：如应用名、网站名称（如：GitHub、微信、阿里云）。
   - **账户标识**：登录用户名、手机号或邮箱地址。
   - **密码/秘钥**：可手动输入，或点击 **“🎲 一键生成”** 自动派生高强度密码。
   - **三级自定义备注**：
     - **备注1**：可填写官方网址、登录入口或主域名；
     - **备注2**：可填写关联备用网址、备选服务或备忘描述；
     - **备注3**：可填写密保问题答案、交易 PIN 码、恢复手机等附加敏感信息。
4. 点击 **“保存新记录”**，数据即刻完成强加密存入本地数据库。

### 4. 两步验证码（TOTP）的导入与使用
- **扫码添加**：在添加 TOTP 时，切换至“扫码识别密钥”标签，可直接使用系统相机扫描第三方网站提供的二维码，或点击“🖼️ 从相册导入图片”自动识别。
- **手动输入**：亦可手动填入 Base32 格式的密钥字符串（支持空格、横杠过滤与大小写自适应容错）。
- **日常查看与复制**：动态口令每 30 秒自动刷新，点击验证码即可安全复制到系统剪贴板。为防止被旁路截获，通知与屏幕 Toast 中绝不打印明文验证码，剪贴板在 45 秒后自动清空。

### 5. 系统自动填充配置与使用
1. 打开系统“设置” $\rightarrow$ “系统” $\rightarrow$ “语言和输入法” $\rightarrow$ “自动填充服务”。
2. 选择本应用（**安全密码箱自动填充**）。
3. 当您在任意受支持的网页或 App 登录界面点击输入框时，键盘上方将弹出填充提示。服务严格匹配包名与 Web 域名等价映射，锁定状态下需重新进行生物识别或主密码授权，防范跨应用与钓鱼嗅探。

### 6. 数据备份、导出与换机迁移
- **加密备份恢复（推荐换机使用）**：
  1. 进入“我的”页面 $\rightarrow$ 找到“加密数据库备份与恢复”；
  2. 点击 **“导出加密备份”**，为当前备份设置一个专用的备份保护密码，保存生成的 `.sqlite` 加密备份文件；
  3. 在新设备上安装本应用，点击 **“导入加密备份”**，输入备份密码，系统将先在内存中进行完整性与密码校验，确认无误后原子还原所有数据。
- **明文 CSV 导入导出**：
  - 点击“明文密码导出”，可生成通用 CSV 文件用于在电脑或其他密码管理软件中查看或迁移。导出前已加入防公式注入转义。
  - *注意：导出的 CSV 文件脱离了保险箱的沙盒保护。因闪存磨损均衡机制，移动设备通常无法保证物理级覆盖擦除，请用户谨慎导出明文 CSV 并妥善保管存储介质。*

---

## 四、 常见问题解答 (FAQ)

**Q1：应用是否真的不需要任何网络？**  
**A**：是的。本应用在 Manifest 清单中彻底移除了 Android 系统的网络权限（`android.permission.INTERNET` 与 `android.permission.ACCESS_NETWORK_STATE`）。无论手机是否开启 Wi-Fi 或移动蜂窝数据，操作系统底层都会物理禁止本应用发起任何网络请求。

**Q2：如果我忘记了主密码，开发者能帮我恢复吗？**  
**A**：**绝对无法恢复**。本应用为纯本地单机架构，所有加密密钥均由您的主密码在本地内存实时派生，开发者与任何第三方均无法访问主密码或保险箱数据。如果您遗忘了主密码，没有任何人能够解密您的本地数据库。

**Q3：换手机时，如何将数据安全迁移到新设备？**  
**A**：由于本应用禁用了 Android 系统的自动云备份（`android:allowBackup="false"`），换机时数据不会自动上云。您只需在旧手机的“我的”页面导出受密码保护的 `.sqlite` 加密备份文件，通过 USB、离线局域网或蓝牙将其传输至新手机，在新手机上点击“导入加密备份”输入密码即可无缝迁移。

**Q4：为什么应用需要相机和生物识别权限？**  
**A**：这些权限均为纯本地功能所需：相机权限仅用于离线扫描 TOTP 二维码（图像在内存解码后立即丢弃，绝不上存或截流）；生物识别权限仅调用硬件安全芯片比对指纹/面容以快速解密，应用绝不触碰原始生物特征。

---

# 📖 English Edition (User Manual)

## 1. Product Positioning & Core Philosophy

**VaultGuard (Offline Standalone Edition)** is a high-security, 100% offline local password and two-factor authentication (2FA/TOTP) manager engineered specifically for data sovereignty and absolute privacy.

- **Zero Network Permission**: The application completely strips and prohibits `android.permission.INTERNET` and `android.permission.ACCESS_NETWORK_STATE` in AndroidManifest.xml. There are zero backend servers, zero remote APIs, and zero analytics trackers.
- **Hardware-Backed Local Authenticated Encryption (AEAD)**: Your Master Key is derived locally from your Master Password via **Argon2id** (RFC 9106) and wrapped inside the hardware keystore enclave (TEE / StrongBox). Vault entries are authenticated and encrypted using **XChaCha20-Poly1305** (default with 24-byte CSPRNG extended nonces) or **AES-256-GCM**.
- **Data Sovereignty**: The developer cannot access your master password or vault contents. Data remains exclusively in your device's isolated application sandbox.
- **Target Audience**: Designed strictly for adult users (**aged 18 and older**) capable of managing digital credentials and disaster recovery.

## 2. Core Features
1. **Four Credential Types**: General Passwords, API Tokens, Crypto Mnemonic Phrases, and RFC 6238 TOTP/2FA codes with millisecond rings.
2. **High-Entropy Password Generator**: Generates custom-length passwords with real-time entropy calculation.
3. **Android Native Autofill Service**: Autofills credentials across apps and browsers with strict anti-phishing domain matching and biometric re-authentication.
4. **Dual Backup System**: Encrypted `.sqlite` backup archives (with atomic integrity verification) and standard CSV import/export (with formula injection mitigations).
5. **Biometric Quick Unlock**: Fast biometric unlock supported by hardware TEE/StrongBox key wrapping with secure master password fallback.

## 3. Backup, Migration & Android System Backup Notice
- **Encrypted Backups (.sqlite)**: Backups are encrypted with independent strong passwords and AEAD integrity tags. Restoring verifies the full file before applying changes atomically.
- **Android Cloud Backup Disabled**: VaultGuard explicitly sets `android:allowBackup="false"` and blocks all cloud backup and device transfer rules to prevent cloud extraction. Transfer to new devices must be performed manually via `.sqlite` encrypted files.
- **Plaintext CSV Warning**: Exported CSV files leave the encrypted sandbox. Flash memory wear leveling prevents physical overwrite guarantees. Handle plaintext exports with extreme care.

## 4. Official Support & Policy Links
- **Support Email**: `freytagnan@proton.me`
- **Source Repository**: `https://github.com/freytagnan-tech/vaultguard_offline_version`
- **Privacy Policy Direct Link**: `https://freytagnan-tech.github.io/public_doc/privacy_policy.html`
