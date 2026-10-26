# Privacy Policy | 隐私政策

**Application Name / 应用名称**: 密码管理器 (密码保险箱 / VaultGuard 离线版)  
**Package Name / 应用包名**: `com.freytagnan.pwdmanager_local`  
**Effective Date / 生效日期**: October 26, 2026 / 2026年10月26日  
**Policy Direct URL / 政策正文直链**: `https://freytagnan-tech.github.io/public_doc/privacy_policy.html`  

---

## 目录 / Table of Contents
1. [中文版隐私政策 (Chinese Version)](#一-中文版隐私政策)
2. [English Privacy Policy (English Version)](#ii-english-privacy-policy)

---

# 一、 中文版隐私政策

### 【引言与核心声明】
欢迎使用密码管理器（VaultGuard 离线版，以下简称“本应用”或“我们”）。
本应用是一款专为极致数据安全而设计的纯本地单机密码与两步身份验证（2FA/TOTP）凭据管理工具。本应用采用“无网络权限”（Zero Network Permission）底层物理隔离设计，在应用程序清单（AndroidManifest.xml）中彻底剥离并移除了所有网络权限（`android.permission.INTERNET` 与 `android.permission.ACCESS_NETWORK_STATE`）。
**本应用及其开发者无法访问您的主密码、解密密钥或保险箱数据，绝不收集、不上传、不共享、不出售您的任何个人数据或敏感凭据。**

请在使用本应用前认真阅读并充分理解本《隐私政策》。您开始使用或继续使用本应用，即表示您理解并认可本政策中关于数据完全本地化、无网络权限、本地认证加密及由您完全掌控数据的全部声明。

### 一、 核心原则：无网络权限与物理级本地沙盒隔离
1. **彻底移除网络权限**：
   本应用在 Android 系统的程序清单中已完全移除网络访问权限指令。Android 系统底层机制物理阻断本应用发起任何网络请求。应用无后端服务器、无云端中继数据库、无远程 API，亦无第三方网络统计组件，数据绝无任何主动外泄通道。
2. **本地认证加密技术（AEAD）规范**：
   - **主凭据加密存储**：所有账号、密码、两步验证密钥、安全备忘及助记词，默认采用高强度 **XChaCha20-Poly1305** 认证加密算法（具备 256 位安全密钥与 24 字节 / 192 位安全随机扩展 Nonce，彻底杜绝 Nonce 碰撞与重用风险）；同时支持用户在设置中选择硬件加速的 **AES-256-GCM** 认证加密算法（使用 12 字节 / 96 位安全随机 Nonce）。解密时均对 128 位认证标签进行常数时间校验，密文或关联数据被篡改将立即阻断解密。
   - **密钥派生函数（KDF）**：采用工业级抗 ASIC/GPU 暴力破解算法 **Argon2id**（RFC 9106 标准，版本 0x13，默认配置 16 MB 内存开销、3 次计算迭代、1 并行度、16 字节 CSPRNG 安全随机盐，结合主密钥 Blake2b 预哈希派生 32 字节 KEK），并提供 PBKDF2-HMAC-SHA256 兼容选项。
   - **根密钥与硬件保护**：在支持硬件安全芯片的设备上优先调用 StrongBox Keymaster 隔离保护；在不支持 StrongBox 的设备上自适应降级至标准 TEE（可信执行环境）或系统级安全 Keystore 隔离保护。生物识别仅充当本地快速解密媒介，生物识别失效时仅允许通过主密码验证，绝无任何后门或绕过逻辑。
   - **加密密钥安全擦除**：数据加密密钥（DEK）仅在应用解锁状态下驻留于本地受保护的安全内存，应用锁屏、后台超时锁定或进程销毁时立即进行多轮覆写清理（Zeroized），密钥不落盘。

### 二、 个人信息“零收集”声明
在使用本应用的过程中，我们承诺：
1. **不收集身份与账户信息**：无需注册任何账号，不要求亦不收集手机号、电子邮箱、姓名、身份证号等；
2. **不收集设备硬件标识符**：不读取亦不收集 IMEI、MEID、Android ID、OAID、MAC 地址、IMSI 或硬件序列号；
3. **不收集用户行为与遥测日志**：无使用时长、点击热力图、页面浏览轨迹等任何统计探针；
4. **不收集地理位置信息**：不申请、不调用 GPS、基站或 Wi-Fi 定位权限；
5. **剪贴板保护机制**：复制凭据仅存入系统临时剪贴板供用户粘贴，适配 Android 13+ 敏感内容标记（`EXTRA_IS_SENSITIVE`），并在 45 秒倒计时后调用系统 API 安全清空剪贴板，绝不后台爬取外部剪贴板内容。

### 三、 本地设备权限申请与最小必要原则
为了在完全断网的前提下提供完备的本地安全体验，应用遵循“最小必要原则”仅在用户主动触发特定功能时申请以下本地权限：
1. **生物识别权限（`android.permission.USE_BIOMETRIC`）**：
   - 使用场景：仅用于提供指纹或面容快速解锁本地密码库。
   - 安全保护：比对由操作系统底层 TEE 硬件执行，应用绝不触碰亦不存储原始生物特征。
2. **相机权限（`android.permission.CAMERA`）**：
   - 使用场景：仅在您主动使用“扫描二维码”添加 2FA 令牌或识别二维码数据时调用。
   - 安全保护：图像帧仅在设备内存中通过离线算法（ML Kit / ZXing）实时解析并即刻释放，绝不将二维码帧、密钥或动态码写入日志、文件缓存或进行截屏留存。
3. **振动权限（`android.permission.VIBRATE`）**：
   - 使用场景：用于扫描成功、复制凭据或长按快捷菜单时的即时触觉反馈。
4. **通知权限（`android.permission.POST_NOTIFICATIONS`，Android 13+）**：
   - 使用场景：仅用于显示剪贴板自动清理倒计时及自动填充捕获新凭证确认提醒。
   - 安全保护：通知采用隐私安全模式（`VISIBILITY_PRIVATE`），锁定状态下不在锁屏显示敏感账号密码。
5. **系统自动填充服务（`AutofillService`）**：
   - 使用场景：用于依据您的指令向其他受支持的应用或浏览器输入框填入对应的账号密码。
   - 安全保护：服务支持严格的应用包名与 Web 域名等价映射，锁定状态下需重新进行生物识别或主密码授权，防范跨应用与钓鱼嗅探。

### 四、 第三方 SDK 与依赖组件说明
本应用彻底剥离了所有商业广告投放 SDK、第三方用户追踪统计 SDK（如友盟、Firebase Analytics、TalkingData、Adjust 等）以及云推送服务。应用内依赖的二维码识别组件（Google ML Kit / ZXing）与 Android Jetpack 基础库均配置为 100% 纯本地离线执行模式，不进行任何远程云端通信。

### 五、 数据自主控制、备份迁移与销毁规范
1. **数据完全自主掌控**：所有凭证数据完整存储于您设备的私有沙盒目录中，用户享有完全掌控、修改和删除的权利。
2. **加密备份（.sqlite）迁移**：应用支持将数据库打包为由独立强密码派生的加密备份文件（.sqlite）。该文件采用 XChaCha20-Poly1305 / AES-256-GCM 认证加密保护，包含格式版本标识与 AAD 完整性校验。恢复导入时采取“先全量解密校验、后原子更新”策略，校验失败绝不破坏当前现有保险箱。“数据不离开设备”是指应用自身绝无主动联网上传行为；用户主动导出的备份文件由用户自主保管或进行冷存储。
3. **CSV 明文导出风险提示**：当您主动选择导出明文 CSV 格式时，导出的明文文件脱离了沙盒环境。因移动设备闪存芯片存在磨损均衡机制（Wear Leveling），移动存储通常无法保证物理级覆盖擦除，请用户谨慎导出明文 CSV 并妥善保管存储介质。
4. **明确 Android 系统备份行为**：本应用在清单中显式配置了 `android:allowBackup="false"`，并在数据提取规则（data extraction rules）中排除了所有数据库、偏好设置和私有文件。系统云备份与设备自动迁移均被彻底禁用，设备重置或系统换机时数据不会自动上云或同步，用户跨设备换机须通过 .sqlite 加密备份文件手动迁移。
5. **数据销毁**：当您在系统设置中执行“清除应用数据”或“卸载本应用”时，操作系统将删除私有沙盒下的全部数据库文件与 Keystore 密钥。

### 六、 目标受众与未成年人保护声明
**本应用专为具备数字资产管理能力、能够独立妥善保管主密码与灾备责任的成年用户（18 岁及以上）设计**。本应用不属于儿童产品，不面向未成年人定向推广，亦不参与 Google Play Families（家庭计划）。应用内未设针对儿童的功能与合规流程，如未成年人确需使用，必须在法定监护人的全程监督与指导下进行。

### 七、 政策更新与联系方式
随着技术更新或法规要求，本隐私政策可能会适时修订。由于本应用无网络推送能力，任何修订都将随应用版本发布完整打包于应用包内部，并同步更新至官方公开直链页面：
- **官方支持与客服邮箱**: `freytagnan@proton.me`
- **开源与问题反馈仓库**: `https://github.com/freytagnan-tech/vaultguard_offline_version`
- **隐私政策正文直链**: `https://freytagnan-tech.github.io/public_doc/privacy_policy.html`

---

# II. English Privacy Policy

### [Core Principles & Privacy Commitment]
Welcome to Password Manager (VaultGuard Offline Edition, hereinafter referred to as "the Application" or "we").
VaultGuard is a 100% offline standalone password and two-factor authentication (2FA/TOTP) management utility engineered specifically for absolute privacy. The application is built on a "Zero Network Permission" architecture. Network permissions (`android.permission.INTERNET` and `android.permission.ACCESS_NETWORK_STATE`) have been completely stripped and prohibited in AndroidManifest.xml.
**The application has zero network communication capabilities. The developer cannot access your master password, decryption keys, or vault data, and will never collect, upload, share, or sell any of your information.**

### 1. Core Principles: Zero Network Permission & Local Sandbox Isolation
1. **Network Permissions Completely Stripped**: The Android OS physically prohibits the application from initiating any network connection. There are no backend servers, cloud relays, remote APIs, or remote telemetry collectors. All data remains exclusively within the protected local application sandbox.
2. **Local Authenticated Encryption (AEAD) Specifications**:
   - **Primary Credential Storage**: Uses **XChaCha20-Poly1305** authenticated encryption by default (256-bit key with 24-byte / 192-bit CSPRNG extended nonce, eliminating nonce reuse vulnerabilities); also supports user-selected hardware-accelerated **AES-256-GCM** (with 12-byte / 96-bit CSPRNG nonce). Decryption performs constant-time 128-bit authentication tag verification; corrupted ciphertexts or mismatched AAD are instantly rejected.
   - **Key Derivation Function (KDF)**: Employs memory-hard **Argon2id** (RFC 9106, Version 0x13, configured by default with 16 MB memory cost, 3 iterations, 1 lane/parallelism, 16-byte random salt, keyed with Blake2b prehash to derive a 32-byte KEK), with PBKDF2-HMAC-SHA256 available for legacy support.
   - **Hardware Key Isolation**: On supported hardware, key wrapping operations leverage StrongBox Keymaster; on devices lacking StrongBox, execution gracefully falls back to the standard Trusted Execution Environment (TEE) or system Keystore. Biometrics serve only as a convenient local unwrap agent; fallback is strictly governed by your Master Password with zero backdoors.
   - **Secure Key Erasure in RAM**: The Data Encryption Key (DEK) resides strictly in volatile memory during unlocked sessions and is immediately zeroized (multiphase overwriting) upon auto-timeout, locking, or process termination.

### 2. "Zero-Collection" Personal Data Declaration
During your use of VaultGuard, we solemnly declare:
1. **No Identity or Account Data**: No registration required; no collection of phone numbers, email addresses, names, or IDs;
2. **No Hardware Identifiers**: No reading or tracking of IMEI, MEID, Android ID, OAID, MAC addresses, or serial numbers;
3. **No Telemetry or Behavioral Logs**: No logging of usage duration, clicks, or screen navigation paths;
4. **No Geolocation Data**: Zero access to GPS, cellular tower, or Wi-Fi positioning services;
5. **Clipboard Protection**: Copied credentials are held temporarily on the system clipboard for immediate pasting, flagged as sensitive (`EXTRA_IS_SENSITIVE` on Android 13+), and securely cleared after 45 seconds via system APIs. Foreign clipboard contents are never inspected.

### 3. Device Permissions & Minimal Privilege Scope
Adhering to the principle of minimal privilege, VaultGuard requests only the following permissions solely when invoked by explicit user actions:
1. **Biometric Authentication (`android.permission.USE_BIOMETRIC`)**: Used strictly to unlock the local database via fingerprint or face match. Biometric comparison occurs entirely inside the device's hardware enclave (TEE); the application never accesses raw biometric templates.
2. **Camera Permission (`android.permission.CAMERA`)**: Invoked strictly when scanning 2FA QR codes. Video frames are decoded in volatile memory using local offline modules (ML Kit / ZXing) and instantly discarded. QR frames, secret keys, and verification codes are never logged or stored in file caches.
3. **Vibration (`android.permission.VIBRATE`)**: Provides instant haptic feedback on successful scans, copies, or long-press interactions.
4. **Notifications (`android.permission.POST_NOTIFICATIONS`, Android 13+)**: Used solely to display clipboard wipe countdowns and autofill credential capture prompts. Notifications use `VISIBILITY_PRIVATE` to prevent credential leakage on lock screens.
5. **Autofill Service (`AutofillService`)**: Assists you in populating login forms in third-party apps and browsers upon direct confirmation. Employs strict package name and web domain mapping with required authentication, mitigating phishing and cross-app snooping.

### 4. Third-Party SDKs & Offline Dependencies
The application completely strips all commercial advertising SDKs, telemetry/analytics libraries (such as Firebase Analytics, Umeng, Adjust), and cloud push frameworks. Built-in barcode recognition libraries run 100% locally on the device CPU/NPU with zero external network access.

### 5. User Data Sovereignty, Backup Migration & Destruction
1. **Full Data Sovereignty**: All credential data resides entirely in your device's isolated application sandbox. You maintain absolute control to modify or delete entries.
2. **Encrypted Backups (.sqlite)**: Backups are protected with a dedicated password, authenticated encryption (XChaCha20-Poly1305 / AES-256-GCM), format versioning, and AAD integrity checks. Restoration uses an atomic replace model that verifies the full archive before touching existing records. "Data never leaves device" specifies that the app will never upload your data; user-exported backups may be stored in cold storage or cloud storage at the user's sole discretion.
3. **Plaintext CSV Caution**: Exported plaintext CSV files leave the encrypted sandbox. Due to hardware flash wear leveling, mobile storage cannot guarantee physical-level overwrite erasure. Users must exercise utmost caution and securely safeguard plaintext files.
4. **Android System Backup Behavior**: The application explicitly specifies `android:allowBackup="false"` and excludes all database, preferences, and private files in data-extraction rules. System auto-backup and device-to-device automatic transfer are completely disabled. Device migration must be performed manually via encrypted .sqlite archives.
5. **Data Destruction**: Executing "Clear Data" or uninstalling the app permanently purges all databases and Keystore entries from the device.

### 6. Target Audience & Children's Privacy Statement
**VaultGuard is engineered strictly for adult users (aged 18 and older)** who manage passwords, API tokens, crypto recovery phrases, and take personal responsibility for disaster recovery. It is not designed for children and does not participate in Google Play Families. Any use by minors must occur under the direct guidance and supervision of a legal guardian.

### 7. Policy Updates & Official Support Channels
Updates to this Privacy Policy will be bundled directly within updated application packages and maintained at our public direct URL:
- **Official Support Email**: `freytagnan@proton.me`
- **Repository & Issue Tracker**: `https://github.com/freytagnan-tech/vaultguard_offline_version`
- **Privacy Policy Direct URL**: `https://freytagnan-tech.github.io/public_doc/privacy_policy.html`
