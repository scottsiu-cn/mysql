# 经典网络平滑迁移到VPC的混访方案 {#concept_ytc_d1y_wdb .concept}

专有网络VPC（Virtual Private Cloud）之间在逻辑上彻底隔离，可以使您在阿里云上构建出一个隔离的网络环境，其安全性及性能都高于经典网络，已成为云上用户首选的网络类型。为满足日益增多的网络迁移需求，RDS新增了网络混访功能，可实现在无闪断、无访问中断的情况下将经典网络平滑迁移到VPC上，且主实例和各只读实例可以分别使用混访方案迁移网络，互不影响。本文将介绍通过RDS管理控制台采用混访方案将经典网络迁移到VPC的操作步骤。

## 背景信息 {#section_lqq_w1y_wdb .section}

以往将RDS实例从经典网络迁移到VPC时，经典网络的内网地址会变为VPC的内网地址（连接字符串没有变化，背后的IP地址有变化），会造成1次30秒内的闪断，而且经典网络中的ECS将不能再通过内网访问该RDS实例，这会对业务产生一定的影响。于是，为能满足平滑迁移网络的需求，RDS新增了混访功能，就提供了这样一个过渡期。

混访是指RDS实例可以同时被经典网络和专有网络中的ECS访问。在混访期间，RDS实例会保留原经典网络的内网地址并新增一个VPC下的内网地址，迁移网络时不会出现闪断。基于安全性及性能的考虑，我们推荐您仅使用VPC，因此混访期有一定的期限，原经典网络的内网地址在保留时间到期后会被自动释放，应用将无法通过经典网络的内网地址访问数据库。为避免对业务造成影响，您需要在混访期中将VPC下的内网地址配置到您所有的应用中，以实现平滑的网络迁移。

例如，某一公司要将经典网络迁移至VPC时，若选用混访的迁移方式，在混访期内，一部分应用通过VPC访问数据库，一部分应用仍通过原经典网络的内网地址访问数据库，等所有应用都可以通过VPC访问数据库时，就可以将原经典网络的内网地址释放掉，如下图所示。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7944/15378020964743_zh-CN.png)

## 功能限制 {#section_tzs_y1y_wdb .section}

在混访期间，有如下功能限制：

-   不支持切换成经典网络。
-   不支持迁移可用区。
-   不支持高可用版及金融版之间的相互切换。

## 前提条件 {#section_rzd_nx2_zdb .section}

-   实例的网络类型是经典网络。

-   实例所在可用区已有可用的VPC和交换机。关于创建VPC和交换机的操作，请参见[管理专有网络](../../../../cn.zh-CN/用户指南/管理专有网络.md)。


## 从经典网络迁移至VPC {#section_cy4_px2_zdb .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。
3.  单击目标实例的ID。
4.  在左侧导航栏中选择**数据库连接**。
5.  单击**切换为专有网络**。
6.  在弹出的对话框中，选择VPC和交换机，然后单击**确定**。
    -   建议选择您的ECS实例所在的VPC，否则ECS实例与RDS实例无法通过内网互通（除非在两个VPC之间创建[高速通道](../../../../cn.zh-CN/快速入门/同账号VPC互连.md)或[VPN网关](../../../../cn.zh-CN/IPsec-VPN入门/配置VPC到VPC连接.md)）。
    -   如果选择的VPC中没有交换机，请创建与实例在同一可用区的交换机。具体操作请参见[管理交换机](../../../../cn.zh-CN/用户指南/管理交换机.md)。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/15378020963260_zh-CN.png)

    -   如果您勾选**保留经典网络**，表示使用混访模式（可以同时被经典网络和VPC的ECS通过内网访问）。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/153780209612640_zh-CN.png)

        |模式|说明|
        |--|--|
        |不使用混访模式|切换为VPC时，RDS实例会有一次30秒的闪断，而且经典网络内网地址会变为VPC内网地址（连接字符串不改变，对应的IP地址改变），因此经典网络的ECS对该RDS实例的内网访问会断开。经典网络的ECS无法再通过内网访问该RDS实例（除非使用[ClassicLink](../../../../cn.zh-CN/用户指南/ClassicLink/ClassicLink概述.md)）。|
        |使用混访模式|切换为VPC时，RDS实例不会发生闪断，原来的经典网络地址保留，同时生成一个新的VPC地址。原来的经典网络ECS仍然可以通过内网正常访问该RDS实例，访问不会中断，直到经典网络地址到期。您需要在经典网络地址到期前将VPC地址配置到您的应用中，以实现业务平滑地迁移到VPC。经典网络地址到期前7天，系统会每天给您账号绑定的手机发送提示短信。|

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/153780209612639_zh-CN.png)


**后续步骤**

-   RDS实例切换为VPC网络后，您需要将VPC的ECS内网IP地址添加到RDS实例的**专有网络白名单分组**。如果没有专有网络的分组，请新建分组。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7943/153780209612638_zh-CN.png)

-   如果不保留经典网络地址，那么在RDS实例切换为VPC网络后，经典网络中的ECS将不能再通过该内网地址访问该RDS实例。经典网络中的ECS需要把数据库连接地址修改为经典网络的RDS的连接地址，或者通过[ClassicLink](../../../../cn.zh-CN/用户指南/ClassicLink/ClassicLink概述.md)连接到VPC的RDS实例，或者[切换到VPC网络](../../../../cn.zh-CN/最佳实践/经典网络迁移到VPC/单ECS迁移示例.md)以连接到VPC的RDS实例。
-   如果保留经典网络地址，该经典网络地址到期后会被自动释放，为避免业务中断，请及时将VPC地址配置到您的应用中。

## 修改原经典网络内网地址的过期时间 {#section_pwp_wx2_zdb .section}

在混访期间，您可以根据需求随时调整保留原经典网络的时间，过期时间会从变更日期重新开始计时。例如，原经典网络的内网地址会在2017年8月18日过期，但您在2017年8月15日将过期时间变更为“14天后”，则原经典网络的内网地址将会在2017年8月29日被释放。

修改过期时间的操作步骤如下所示：

1.  登录[RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。
3.  单击目标实例的ID。
4.  在左侧导航栏中，选择**数据库连接**。
5.  在实例连接标签页中，单击**修改过期时间**，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7944/15378020964748_zh-CN.png)

6.  在修改过期时间的确认页面，选择过期时间，单击**确定**。

