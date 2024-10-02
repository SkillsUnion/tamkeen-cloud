# Amazon Machine Images in Amazon EC2

An Amazon Machine Image (AMI) is a pre-configured image that provides the necessary software to set up and boot an Amazon EC2 instance. Each AMI also includes a block device mapping that specifies the block devices to attach to the instances upon launch. When launching an instance, it is mandatory to specify an AMI that is compatible with the chosen instance type. AMIs can be sourced from AWS-provided options, public AMIs, AMIs shared by others, or AMIs purchased from the AWS Marketplace.

An AMI is specific to the following attributes:

- **Region**
- **Operating System**
- **Processor Architecture**
- **Root Device Type**
- **Virtualization Type**

Multiple instances can be launched from a single AMI when uniform configurations are needed. Conversely, different AMIs can be used to launch instances with varying configurations, as illustrated below.

![Launch multiple instances from an AMI.](ami-multiple-instances.png)

It is possible to create an AMI from an existing Amazon EC2 instance and subsequently use it to launch instances with the same configuration. AMIs can also be copied to different AWS Regions, allowing instances to be launched in those Regions. Additionally, AMIs that are created can be shared with other AWS accounts, enabling them to launch instances with the same configuration. Furthermore, AMIs can be sold through the AWS Marketplace.

## AMI Types and Characteristics in Amazon EC2

When launching an instance, it is essential to select an Amazon Machine Image (AMI) that is compatible with the chosen instance type. The characteristics to consider when selecting an AMI include:

- **Region**
- **Operating System**
- **Processor Architecture**
- **Launch Permissions**
- **Root Device Type**
- **Virtualization Types**

### Launch Permissions

The availability of an AMI is determined by the owner through launch permissions, which fall into the following categories:

| Launch Permission | Description |
| ----------------- | ----------- |
| **Public**         | The owner grants launch permissions to all AWS accounts. |
| **Explicit**       | The owner grants launch permissions to specific AWS accounts, organizations, or organizational units (OUs). |
| **Implicit**       | The owner has implicit launch permissions for an AMI. |

Amazon and the Amazon EC2 community provide a broad selection of public AMIs. Developers can also charge for their AMIs via the AWS Marketplace.

### Root Device Type

AMIs are categorized into two types based on their root device:

- **Amazon EBS-backed AMI**: The root device for an instance launched from this AMI is an Amazon Elastic Block Store (Amazon EBS) volume created from an EBS snapshot. This type is supported for both Linux and Windows AMIs.
  
- **Amazon Instance Store-backed AMI**: The root device for an instance launched from this AMI is an instance store volume created from a template stored in Amazon S3. This type is supported only for Linux AMIs.

#### Comparison of AMI Types

| Characteristic                 | Amazon EBS-backed AMI                         | Amazon Instance Store-backed AMI                |
| ------------------------------ | --------------------------------------------- | ----------------------------------------------- |
| **Root Device Volume**          | EBS volume                                    | Instance store volume                           |
| **Boot Time for an Instance**   | Usually less than 1 minute                    | Usually less than 5 minutes                     |
| **Data Persistence**            | Root volume is deleted upon instance termination by default. Data on other EBS volumes persists. | Data persists only during the life of the instance. |
| **Stopped State**               | Can be stopped; root volume persists in EBS.  | Cannot be stopped; instances are either running or terminated. |
| **Modifications**               | Instance type, kernel, RAM disk, and user data can be changed while the instance is stopped. | Instance attributes are fixed for the life of an instance. |
| **Charges**                     | Instance usage, EBS volume usage, and storing AMI as an EBS snapshot. | Instance usage and storing AMI in Amazon S3. |
| **AMI Creation/Bundling**       | Uses a single command/call                    | Requires installation and use of AMI tools      |

### Virtualization Types

Amazon Machine Images use one of two types of virtualization: **Paravirtual (PV)** or **Hardware Virtual Machine (HVM)**. The main differences between PV and HVM AMIs lie in their boot process and their ability to leverage special hardware extensions (CPU, network, and storage) for enhanced performance. Windows AMIs are HVM AMIs.

#### Comparison of Virtualization Types

| Characteristic                  | HVM                                              | PV                                               |
| --------------------------------| ------------------------------------------------ | ------------------------------------------------ |
| **Description**                 | HVM AMIs boot by executing the master boot record of the root block device of your image. They provide the ability to run an OS directly on a virtual machine, similar to running on bare-metal hardware. | PV AMIs boot with a special boot loader called PV-GRUB, which starts the boot cycle and then chain loads the kernel specified in the menu.lst file on your image. |
| **Supported Instance Types**    | Supported by all current generation instance types. | Supported by previous generation instance types: C1, C3, M1, M3, M2, and T1. |
| **Support for Hardware Extensions** | HVM guests can leverage hardware extensions for enhanced networking and GPU processing, providing fast access to the underlying hardware. | PV guests cannot use hardware extensions like enhanced networking or GPU processing. |
| **How to Find**                 | Verify that the virtualization type is set to HVM using the console or the `describe-images` command. | Verify that the virtualization type is set to Paravirtual using the console or the `describe-images` command. |

#### PV on HVM

Traditionally, paravirtual guests performed better with storage and network operations due to special drivers that avoided the overhead of emulating hardware. Now, PV drivers are available for HVM guests, enabling them to achieve similar or better performance compared to paravirtual guests.
