---
categories: [dev, linux, lpic-1]
date: '2018-12-12 13:55:23'
tags: [dev, linux, lpic-1]
title: LPIC-1 Linux 管理员
updated: '2018-12-21 12:47:53'
...
---
# LPIC-1 Linux 管理员
<!-- MarkdownTOCs -->

- [系统架构](./architecture/index_architecture.md "System Architecture")
- [Linux安装和包管理](./installation/index_installation.md "Linux Installation and Package Management")
- [命令行和GNU](./commands-and-gnu/index_commands-and-gnu.md "GNU and Unix Commands")
    - [流 & 管道 & 重定向](./commands-and-gnu/streams-pipes-redirects.md "04 streams & pipes & redirects")
- [文件系统 & FHS & 设备](./filesystems/index_filesystems.md "Devices & Linux Filesystems & Filesystem Hierarchy Standard")
    - [管理文件权限和所有权](./filesystems/file-permissions.md "04 Manage file permissions and ownership")
- [Shell和Shell脚本](./shell/index_shell.md "Shells and Shell Scripting")
- [用户接口和桌面](./interfaces/index_interfaces.md "Interfaces and Desktops")
- [管理任务](./administrative/index_administrative.md "Administrative Tasks")
- [基本系统服务](./system-services/index_system-services.md "Essential System Services")
- [网络基础](./networking/index_networking.md "Networking Fundamentals")
- [安全性](./security/index_security.md "Security")

<!-- /MarkdownTOCs -->
[回到系列教程主目录](./index.md)

> LPI致力于开发Linux认证的全球标准。
> LPI是开源专业人士的全球认证标准和职业支持组织。 
> 凭借超过600,000考试，它是世界上第一个也是最大的供应商中立的Linux和开源认证机构。

LPIC-1 认证涉及两个考试：考试 101 和考试 102。要获得 LPIC-1 认证，您必须通过考试 101 和考试 102。

参考:
-   [LPI官网](https://www.lpi.org/zh-CN/)
-   [IBM Developer LPIC-1 学习资料](https://www.ibm.com/developerworks/cn/linux/l-lpic1-v3-map/)

```yaml
- ['index_architecture.md'            , '系统架构'                           , 'System Architecture']
- [    'hardware-settings.md'         , '确定和配置硬件设置'                 , '01 Determine and configure hardware settings']
- [    'boot-the-system.md'           , '引导系统'                           , '02 Boot the system']
- [    'runlevels-shutdown-system.md' , '修改运行级别并关闭或重启系统'       , '03 Change runlevels boot targets and shutdown or reboot system']
- ['index_installation.md'            , 'Linux安装和包管理'                  , 'Linux Installation and Package Management']
- [    'hard-disk-layout.md'          , '设计硬件布局'                       , '01 Design hard disk layout']
- [    'boot-manager.md'              , '安装引导管理器'                     , '02 Install a boot manager']
- [    'shared-libraries.md'          , '管理共享库'                         , '03 Manage shared libraries']
- [    'package-management.md'        , 'Debian 包管理'                      , '04 Use Debian package management']
- [    'rpm-and-yum.md'               , 'RPM 和 YUM 包管理'                  , '05 Use RPM and YUM package management']
- [    'virtualization.md'            , '虚拟化技术'                         , '06 Linux as a virtualization guest']
- ['index_commands-and-gnu.md'        , '命令行和GNU'                        , 'GNU and Unix Commands']
- [    'command-line.md'              , '命令行'                             , '01 Work on the command line']
- [    'text-streams-filters.md'      , '过滤器处理文本流'                   , '02 Process text streams using filters']
- [    'file-management.md'           , '执行基本的文件和目录管理'           , '03 Perform basic file management']
- [    'streams-pipes-redirects.md'   , '流 & 管道 & 重定向'                 , '04 streams & pipes & redirects']
- [    'processes.md'                 , '创建监视和终止进程'                 , '05 Create monitor and kill processes']
- [    'process-priorities.md'        , '修改进程执行优先级'                 , '06 Modify process execution priorities']
- [    'regular-Search-text-files.md' , '正则表达式搜索文本文件'             , '07 Search text files using regular expressions']
- [    'file-editing.md'              , '文本编辑 vi'                        , '08 Basic file editing']
- ['index_filesystems.md'             , '文件系统 & FHS & 设备'              , 'Devices & Linux Filesystems & Filesystem Hierarchy Standard']
- [    'filesystems-partitions.md'    , '创建分区和文件系统'                 , '01 Create partitions and filesystems']
- [    'integrity-of-filesystems.md'  , '维护文件系统的完整性'               , '02 Maintain the integrity of filesystems']
- [    'control-filesystems.md'       , '控制文件系统的装载和卸载'           , '03 Control mounting and unmounting of filesystems']
- [    'file-permissions.md'          , '管理文件权限和所有权'               , '04 Manage file permissions and ownership']
- [    'hard-and-symbolic-links.md'   , '创建和修改硬链接和符号链接'         , '05 Create and change hard and symbolic links']
- [    'find-system-files.md'         , '查找系统文件并将文件放到正确的位置' , '06 Find system files and place files in the correct location']
- ['index_shell.md'            , 'Shell和Shell脚本'      , 'Shells and Shell Scripting']
- ['index_interfaces.md'       , '用户接口和桌面'        , 'Interfaces and Desktops']
- ['index_administrative.md'   , '管理任务'              , 'Administrative Tasks']
- ['index_system-services.md'  , '基本系统服务'          , 'Essential System Services']
- ['index_networking.md'       , '网络基础'              , 'Networking Fundamentals']
- ['index_security.md'         , '安全性'                , 'Security']
```
