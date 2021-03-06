# Enable ECS instances to access the Internet with SNAT

This topic describes how to configure Source Network Address Translation \(SNAT\) for a NAT gateway. SNAT enables Elastic Compute Service \(ECS\) instances to access the Internet when the ECS instances are not assigned static public IP addresses or elastic IP addresses \(EIPs\).

## Scenario

The following scenario is used as an example. For example, a company creates a Virtual Private Cloud \(VPC\) network and a VSwitch on Alibaba Cloud. Multiple ECS instances are attached to the VSwitch. The ECS instances are not assigned static public IP addresses or EIPs. To meet business requirements, the company needs all ECS instances to be able to access the Internet.

You can configure SNAT for a NAT gateway to allow all ECS instances in a VPC network to access the Internet when the ECS instances are not assigned static public IP addresses or EIPs.

![Scenario](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7738039951/p149166.png)

## Prerequisites

Before you start, make sure that the following requirements are met:

-   An Alibaba Cloud account is created. If you do not have an Alibaba Cloud account, click [Create an Alibaba Cloud account](https://account.alibabacloud.com/register/intl_register.htm).
-   A VPC network and a VSwitch are created. For more information, see [Create a VPC](/intl.en-US/VPCs and VSwitches/VPC management/Create a VPC.md).
-   An EIP is created in the region where the NAT gateway to be associated with the EIP is deployed. For more information, see [Apply for new EIPs](/intl.en-US/User Guide/Create an EIP/Apply for new EIPs.md).

## Procedure

![Procedure](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7738039951/p149588.png)

## Step 1: Create a NAT gateway

NAT gateway is an enterprise-class gateway that provides address translation services for Internet access. You must create a NAT gateway before you create a SNAT entry.

Perform the following steps to create a NAT gateway:

1.  Log on to the [NAT Gateway console](https://vpc.console.aliyun.com/nat).

2.  On the **NAT Gateway** page, click **Create NAT Gateway**.

3.  In the **Create NAT** dialog box, set the following parameters, click **Buy Now**, and complete the payment.

    -   **Region and Zone**: Select the region and zone where you want to deploy the NAT gateway.

        **Note:** An enhanced NAT gateway can be created only in China \(Hohhot\), China \(Chengdu\), UK \(London\), Germany \(Frankfurt\), Malaysia \(Kuala Lumpur\), Singapore, and India \(Mumbai\).

    -   **VPC ID**: Select the VPC network in which the NAT gateway is created. After the NAT gateway is created, you cannot change the VPC network in which the NAT gateway is deployed.

        **Note:** If you cannot find the VPC network that you want to manage in the list, perform the following operations:

        -   Check whether the VPC network is already associated with a NAT gateway. Each VPC network can be associated with only one standard NAT gateway.
        -   Check whether the VPC network has a custom route entry with the destination CIDR block set to 0.0.0.0/0. If such a custom route entry exists, delete it.
        -   If your account is a Resource Access Management \(RAM\) user, check whether the RAM user is authorized to access the VPC network. If the RAM user is not authorized, contact the owner of the Alibaba Cloud account that creates the RAM user to grant permissions.
    -   **VSwitch ID**: Select the VSwitch to which the NAT gateway is attached.

        **Note:** This parameter is available only when you create an enhanced NAT gateway.

    -   **NAT Type**: Select the type of the NAT gateway that you want to create.

        -   **Standard**
        -   **Enhanced**
        Enhanced NAT gateways support all features of standard NAT gateways. Compared with standard NAT gateways, enhanced NAT gateways use an upgraded technical architecture. This ensures higher elasticity and stability and helps you better manage network traffic sent over the Internet. **Enhanced** is selected in this topic.

    -   **Specification**: Select a specification for the NAT gateway.

        -   **Small**
        -   **Medium**
        -   **Large**
        -   **Super Large-1**
        The size of a NAT gateway determines its SNAT performance, including the maximum concurrent connections and the number of new connections per second. However, the size does not affect the DNAT performance. For more information, see [Compare NAT gateway sizes](/intl.en-US/NAT Gateway Instance/Types of NAT gateway.md).

        **Small** is selected in this topic.

    -   **Billing Method**: Select a billing method.

        Only pay-by-specification is supported. For more information, see [Pay-by-specification](/intl.en-US/Pricing/Pay-as-you-go.md).

    -   **Billing Cycle**: Displays the billing cycle.

After you create a NAT gateway, you can view the NAT gateway on the **NAT Gateway** page.

![Create a NAT gateway](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8458039951/p149224.png)

## Step 2: Associate the NAT gateway with an EIP

A NAT gateway functions as expected only after it is associated with an EIP. After you create a NAT gateway, you can associate it with an EIP.

Perform the following steps to associate the NAT gateway with an EIP:

1.  On the **NAT Gateway** page, find the NAT gateway created in Step 1, and choose **![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8458039951/p103337.png)** \> **Bind Elastic IP Address** in the **Actions** column.

2.  In the Bind Elastic IP Address dialog box, set the following parameters, and click **OK**.

    -   **Usable EIP List**: Select the EIP that you want to associate with the NAT gateway.
    -   **VSwitch**: Select the VSwitch for which you want to add SNAT entries.

        The system automatically adds SNAT entries for the VSwitch so that Alibaba Cloud services connected to this VSwitch can access the Internet. You can also skip this step and manually add SNAT entries after you associate an EIP with the NAT gateway.

        No VSwitch is selected in this topic.

        **Note:** This parameter is available only for NAT gateways that are not associated with EIPs.


## Step 3: Create a SNAT entry

SNAT enables ECS instances in a VPC network to access the Internet through a NAT gateway when these ECS instances are not assigned static public IP addresses or EIPs.

Perform the following steps to create a SNAT entry:

1.  On the **NAT Gateway** page, find the NAT gateway created in Step 1, and click **Configure SNAT** in the **Actions** column.

2.  In the **Used in SNAT Entry** section, click **Create SNAT Entry**.

3.  In the **Create SNAT Entry** dialog box, set the following parameters:

    **VSwitch Granularity** is used as an example to describe how to create a SNAT entry for a VSwitch.

    -   **VSwitch**: Select a VSwitch in a VPC network. All ECS instances attached to the VSwitch can access the Internet with SNAT.
    -   **VSwitch CIDR Block**: displays the CIDR block of the VSwitch.
    -   **Public IP Address**: the EIP that is used to access the Internet.

        **Note:** An EIP that has been used in a DNAT entry cannot be used in a SNAT entry.

    -   **Entry Name**: Enter a name for the SNAT entry.

        The name must be 2 to 128 characters in length, and can contain letters, Chinese characters, digits, underscores \(\_\), and hyphens \(-\). It must start with a letter or Chinese character.

4.  Click **OK**.


## Step 4: Test the network connectivity

After you create a SNAT entry, you can test the network connectivity between the ECS instance and the Internet.

**Note:** Make sure that the security group rules of the ECS instance allow the ECS instance to access the Internet.

In this example, an ECS instance that runs a Linux operating system is used to test the network connectivity.

1.  Log on to the ECS instance that is attached to the VSwitch.

2.  Run the `ping` command to test the network connectivity.

    The test result shows that the ECS instance can access the Internet.

    ![Test the network connectivity](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8738039951/p149291.png)


