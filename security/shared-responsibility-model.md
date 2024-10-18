### **The AWS Shared Responsibility Model**

The AWS Shared Responsibility Model outlines the division of responsibilities between AWS and its customers regarding security. Both parties play a role in maintaining the security and protection of resources within the AWS environment. This model is split into two main categories: **security in the cloud** (customer responsibilities) and **security of the cloud** (AWS responsibilities).

![alt text](image.png)

---

#### **Customer Responsibilities: Security in the Cloud**

Customers are responsible for securing the resources they create and manage within the AWS Cloud. This includes:

- **Data and Content Control**: Customers have full control over the content they store in AWS, including deciding what to store and who has access to it.
- **Managing Access**: You are responsible for defining who has access to your resources and how access rights are granted, managed, and revoked.
- **Operating System and Security Configuration**: This involves configuring and patching operating systems running on services like Amazon EC2 instances.
- **Security Group and Network Management**: You must configure security groups and other network-related security settings to control access to your resources.
- **Account Management**: It is your responsibility to manage and secure user accounts and permissions in AWS.

In summary, the security of what you build, store, and manage in the cloud is your responsibility.

---

#### **AWS Responsibilities: Security of the Cloud**

AWS is responsible for securing the infrastructure that runs the services in the AWS Cloud. This includes:

- **Physical Security**: AWS secures the physical data centers, ensuring protection through access controls, monitoring, and various other physical safeguards.
- **Network and Virtualization Infrastructure**: AWS manages and protects the network infrastructure, including the hardware and software needed to deliver AWS services.
- **Global Infrastructure**: AWS secures the Regions, Availability Zones, and edge locations that make up the AWS Cloud infrastructure.

AWS handles the security of the infrastructure that supports your resources, ensuring a secure foundation for services.

---

#### **Analogy: Homeowner and Homebuilder**

You can think of the shared responsibility model as similar to the relationship between a homeowner and a homebuilder. AWS (the builder) constructs and secures the infrastructure (the house). The customer (the homeowner) is responsible for securing the content inside (e.g., locking the doors and securing belongings). Both parties work together to ensure overall security.

By adhering to the shared responsibility model, AWS ensures the cloud's infrastructure is secure, while customers maintain control and security of their data and applications within that environment.