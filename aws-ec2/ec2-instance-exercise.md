# Finding an Amazon EC2 Instance Type

Before launching an EC2 instance, it is essential to select an instance type that matches the specific needs of your workload. The choice of instance type may depend on various resources required by your application, such as compute, memory, or storage. It is advisable to identify multiple instance types that might suit your workload and to evaluate their performance in a test environment. There is no substitute for measuring the performance of your application under actual load conditions.

To assist in selecting the appropriate instance type, you can use the **EC2 Instance Type Finder** for suggestions and guidance. For more information, refer to the documentation on how to [Get recommendations from EC2 instance type finder](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-type-recommendations.html).


### 1. Find an Instance Type Using the Console

The Amazon EC2 console provides a user-friendly interface to help you find an instance type that meets your needs.

#### To Find an Instance Type Using the Console:

1. Open the Amazon EC2 console at [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).

2. From the navigation bar, select the Region where you plan to launch your instances. You can choose any available Region, regardless of your geographical location.

3. In the navigation pane, select **Instance Types**.

4. (Optional) Click on the preferences (gear) icon to choose which instance type attributes to display, such as On-Demand Linux pricing. Then, click **Confirm**. Alternatively, you can select the name of an instance type to open its details page, where you can view all attributes available through the console. Note that the console might not display all attributes that are available through the API or the command line.

5. Use the instance type attributes to filter the list of displayed instance types according to your needs. You can filter by attributes such as:
   - **Availability Zones**: The name of the Availability Zone, Local Zone, or Wavelength Zone.
   - **vCPUs or Cores**: The number of vCPUs or cores available.
   - **Memory (GiB)**: The memory size, measured in GiB.
   - **Network Performance**: The network performance, measured in Gigabits.
   - **Local Instance Storage**: Whether the instance type includes local instance storage (`true | false`).

6. (Optional) To see a side-by-side comparison of multiple instance types, select the checkboxes for the instance types you wish to compare. The comparison will be displayed at the bottom of the screen.

7. (Optional) To save the list of instance types for further review, select **Actions** and then choose **Download list CSV**. This action will download a comma-separated values (.csv) file containing all instance types that match your selected filters.

8. (Optional) To launch instances using an instance type that meets your needs, select the checkbox for the desired instance type and choose **Actions**, then **Launch instance**. For more details on launching instances, refer to the guide on [Launching an EC2 Instance Using the Launch Instance Wizard in the Console](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/launching-instance.html).