# User Service Agreement | 用户服务协议

**Application Name / 应用名称**: 密码管理器 (密码保险箱 / VaultGuard 离线版)  
**Package Name / 应用包名**: `com.freytagnan.pwdmanager_local`  
**Effective Date / 生效日期**: October 26, 2026 / 2026年10月26日  
**Official Support / 客服邮箱**: `freytagnan@proton.me`  
**Repository / 官方仓库**: `https://github.com/freytagnan-tech/vaultguard_offline_version`  

---

## 目录 / Table of Contents
1. [中文版用户服务协议 (Chinese Version)](#一-中文版用户服务协议)
2. [English User Service Agreement (English Version)](#ii-english-user-service-agreement)

---

# 一、 中文版用户服务协议

### 【重要提示】
欢迎使用密码管理器（VaultGuard 离线版，以下简称“本应用”或“本软件”）。
本协议是您（以下亦称“用户”）与本软件开发者之间关于下载、安装、使用本软件所订立的具有法律效力的协议。
请您在安装或使用本应用前，仔细阅读并充分理解本协议全部条款，特别是免除或限制责任的条款、主密码不可找回警示、目标受众限定以及用户安全责任条款。如您不同意本协议的任何条款，请勿安装、使用或立即卸载本软件。当您开始使用或继续使用本软件，即视为您已完全知悉并同意受本协议各项条款的约束。

### 一、 服务定位与软件功能
1. **本地单机工具定位**：
   本软件是一款基于现代密码学架构开发的纯本地单机个人密码与凭据管理安全工具。本软件为用户提供本地数据强加密存储、主密码校验、双重身份验证（2FA/TOTP）本地计算、多格式凭据管理、数据离线导入导出及系统级安全自动填充等功能。
2. **零网络权限与物理隔离**：
   本软件在程序清单（AndroidManifest.xml）中彻底剥离了 `android.permission.INTERNET` 与 `android.permission.ACCESS_NETWORK_STATE` 权限，不提供任何云端服务器托管、远程数据同步、在线账户注册或远程身份验证服务。所有操作与数据处理均在您持有的物理终端设备本地独立完成。

### 二、 目标受众与未成年人限制
**本软件专为具备数字资产管理能力、能够独立妥善保管主密码与承担灾备责任的成年用户（18 岁及以上）设计**。本软件不属于儿童产品，不面向未成年人定向推广，亦未加入 Google Play Families 计划。如未成年人确需使用本软件，必须在法定监护人的全程监督与指导下进行。

### 三、 主密码管理与用户核心安全责任【特别警示】
1. **纯本地密钥管理与不可找回原则**：
   本软件采用纯本地架构。您的主密码是派生数据解密密钥（DEK）的唯一核心凭据，开发者与任何第三方均无法访问您的主密码、解密密钥或保险箱数据。本软件不提供、亦在技术上无法提供“找回密码”、“重置密码”或“人工申诉解密”功能。
2. **主密码保管责任**：
   您必须牢记并妥善保管您的主密码。一旦主密码遗忘、丢失或损坏，您加密存储于本软件中的所有数据将永久无法解密和恢复，开发者在技术上与法律上均无法协助您找回数据，由此产生的一切损失和后果由您自行承担。
3. **物理与系统环境安全**：
   您应确保安装本软件的设备处于安全受控状态，防范手机遗失、恶意软件感染、Root 提权攻击或物理被盗风险。若因您自身设备越狱/Root、遭受木马病毒入侵、将主密码告知他人或锁屏密码泄露导致的资产损失，由您自行承担责任。

### 四、 数据所有权、导出与备份规范
1. **数据完全所有权**：
   您在本软件中录入、存储、导入的全部账号、密码、密钥及文字记录等数据，其完整所有权与控制权均归属于您。开发者不主张亦不拥有您任何数据的任何权益。
2. **禁用系统备份与手动迁移**：
   本软件显式配置了 `android:allowBackup="false"`，并排除了所有系统云备份与设备自动迁移数据。为防范设备遗失、系统损坏或换机导致数据丢失，您须定期使用应用内加密备份功能导出 `.sqlite` 文件并妥善保存。
3. **明文导出风险自负**：
   若您选择将本地数据导出为明文 CSV 格式，该文件将完全脱离本软件的加密保护机制。因闪存磨损均衡（Wear Leveling）机制限制，移动存储通常无法保证物理级覆盖擦除，您须承担导出明文文件后的保密与介质保管义务。

### 五、 免责声明与技术责任限制
1. 本软件按“现状”（AS IS）提供，不包含任何明示或暗示的保证。
2. 在法律允许的最大范围内，开发者不对因不可抗力、用户设备硬件损坏、系统崩溃、主密码遗忘、恶意第三方软件攻击或明文导出泄露所造成的任何直接或间接数据损失承担法律赔偿责任。

### 六、 联系我们
如对本协议有任何疑问，请通过以下方式联系：
- 客服支持邮箱: `freytagnan@proton.me`
- 官方项目仓库: `https://github.com/freytagnan-tech/vaultguard_offline_version`

---

# II. English User Service Agreement

### [IMPORTANT NOTICE]
Welcome to Password Manager (VaultGuard Offline Edition, hereinafter referred to as "the Application" or "the Software").
This Agreement is a legally binding contract between you (the "User") and the developer. By installing, copying, or using this application, you agree to be bound by the terms of this Agreement. If you do not agree to all terms herein, do not install or use the Software.

### 1. Scope of Service & Architecture
1. **Standalone Offline Utility**: VaultGuard is a 100% offline password and credential management utility. It performs local authenticated encryption (AEAD), master password verification, RFC 6238 TOTP computation, and native autofill.
2. **Zero Network Permissions**: Network access permissions (`INTERNET` and `ACCESS_NETWORK_STATE`) have been entirely stripped from AndroidManifest.xml. The application maintains no servers, APIs, or telemetry endpoints.

### 2. Target Audience & Age Restrictions
**VaultGuard is engineered strictly for adult users (aged 18 and older)** capable of managing digital credentials and disaster recovery responsibilities. It does not target minors and does not participate in Google Play Families.

### 3. Master Password & Data Loss Warning
1. **No Password Recovery**: Your Master Password is the sole component from which decryption keys are derived. The developer cannot access your master password or vault data. No backdoors, master resets, or cloud recovery mechanisms exist.
2. **User Responsibility**: If you lose or forget your Master Password, your data is permanently lost and mathematically unrecoverable.

### 4. Backups, Android System Backup & Disclaimers
1. **Android Backup Disabled**: VaultGuard sets `android:allowBackup="false"` to prevent automated cloud uploads. Transfer to new devices must be performed manually via `.sqlite` encrypted files.
2. **CSV Plaintext Warning**: Plaintext CSV exports leave the encrypted sandbox. Hardware wear leveling prevents physical overwrite guarantees. Safeguard exported files diligently.
3. **Limitation of Liability**: To the maximum extent permitted by applicable law, the software is provided "AS IS", without warranties of any kind. The developer shall not be liable for any damages resulting from forgotten passwords, device failure, or compromised operating systems.

### 5. Support & Inquiries
- Official Support Email: `freytagnan@proton.me`
- Official Repository: `https://github.com/freytagnan-tech/vaultguard_offline_version`
