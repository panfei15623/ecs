# 扩展分区和文件系统\_Windows {#concept_rjc_l5h_ydb .concept}

扩容云盘只是扩大存储容量，不会扩容文件系统。您需要参照本文描述自行格式化新增的存储容量，以便扩展存储空间。

## 扩容指引 {#section_hst_vj1_qgb .section}

本文仅适用于状态为**使用中**的云盘，且所挂载的实例状态为**运行中**。

-   对于待挂载数据盘，请参见[挂载云盘](cn.zh-CN/块存储/云盘/挂载云盘.md#)和[分区格式化数据盘](../../../../cn.zh-CN/个人版快速入门/步骤 4：格式化数据盘/Windows格式化数据盘.md#)。
-   数据盘扩容后容量大于2048 GiB时，您必须使用GPT分区格式。如果您已经使用了MBR分区格式，但无需保留数据盘上的数据，请参见[Windows实例更换分区格式步骤](cn.zh-CN/块存储/云盘/分区格式化数据盘/分区格式化大于2 TiB云盘.md#Windows2012Snapshot)。

## 准备工作 {#section_fds_2m1_qgb .section}

1.  通过ECS控制台或者API扩容云盘。
2.  [创建快照](cn.zh-CN/快照/使用快照/创建快照.md#)以备份数据。
3.  云盘已挂载到实例上，实例已处于**运行中**状态。
4.  数据盘已完成分区格式化。具体操作请参见[分区格式化数据盘](../../../../cn.zh-CN/个人版快速入门/步骤 4：格式化数据盘/Windows格式化数据盘.md#)。

## 扩展系统盘分区 {#section_h4v_txm_qgb .section}

在ECS控制台上扩容系统盘后，对应系统盘分区的文件系统并未扩容。您需要连接实例扩容文件系统。本示例中以Windows Server 2008 R2企业版64位中文版操作系统为例。扩容前的系统盘容量为50 GiB，扩容为72 GiB，文件系统类型为NTFS。

1.  [远程连接Windows实例](cn.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md#)。
2.  打开服务器管理器。
3.  在左侧导航栏中，选择**存储** \> **磁盘管理**。
4.  选择**操作** \> **刷新**或**操作** \> **重新扫描磁盘** 。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490641660_zh-CN.png)

5.  在磁盘管理区域，查看未分配容量。本例中，**磁盘 0**是扩容的系统盘。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490641658_zh-CN.png)

6.  右键单击**磁盘 0**主分区的空白处，并选择**扩展卷**。
7.  根据扩展卷向导的指示完成扩展卷操作。

    完成后，新增空间会自动合入原来的卷中，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490641657_zh-CN.png)


## 扩展数据盘分区 {#section_hbw_5lw_dhb .section}

在ECS控制台上扩容数据盘后，数据盘的每个分区的文件系统并未扩容。您需要连接实例扩容文件系统。本示例中以Windows Server 2008 R2企业版64位中文版操作系统为例。扩容前的数据盘容量为80 GiB，扩容为120 GiB，文件系统类型为NTFS。

1.  [远程连接Windows实例](cn.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md#)。
2.  打开服务器管理器。
3.  在左侧导航栏中，选择**存储** \> **磁盘管理**。
4.  选择**操作** \> **刷新**或**操作** \> **重新扫描磁盘**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490641660_zh-CN.png)

5.  在磁盘管理区域，查看未分配的数据盘容量。本例中，**磁盘 1**是扩容的数据盘。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490641665_zh-CN.png)

6.  扩展**磁盘 1**。
    -   选项一：如果新磁盘空间用于扩容已有的分区，按照以下步骤完成扩容：
        1.  右键单击**磁盘1**主分区的空白处，并选择**扩展卷**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490641661_zh-CN.png)

        2.  根据扩展卷向导的指示完成扩展卷操作。

            完成后，新增的数据盘空间会自动合入原来的卷中。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490741662_zh-CN.png)

    -   选项二：如果新磁盘空间用于增加新的分区，按照以下步骤完成扩容：
        1.  右键单击**磁盘1**未分配区的空白处，并选择**新建简单卷**。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490741663_zh-CN.png)

        2.  根据新建简单卷向导的指示完成扩展卷操作。

            完成后，新增的数据盘空间会新建一个分区。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155978490741664_zh-CN.png)


## 相关操作 {#section_d38_a4a_c0r .section}

-   [扩展文件系统\_Linux系统盘](cn.zh-CN/块存储/云盘/扩容云盘/扩展分区与文件系统_Linux系统盘.md#)
-   [扩展文件系统\_Linux数据盘](cn.zh-CN/块存储/云盘/扩容云盘/扩展分区与文件系统_Linux数据盘.md#)

