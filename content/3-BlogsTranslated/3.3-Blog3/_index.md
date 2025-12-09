---
title: "Deploying Advanced AWS Graviton Adoption Strategies Across AWS Regions"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

**Deploying Advanced AWS Graviton Adoption Strategies Across AWS Regions**

By Matt Howard | on August 26, 2025 | in [Advanced (300)](https://aws.amazon.com/blogs/compute/category/learning-levels/advanced-300/), [Amazon EC2](https://aws.amazon.com/blogs/compute/category/compute/amazon-ec2/), [Best Practices](https://aws.amazon.com/blogs/compute/category/post-types/best-practices/), [Graviton](https://aws.amazon.com/blogs/compute/category/compute/graviton/) | [Permalink](https://aws.amazon.com/blogs/compute/implementing-advanced-aws-graviton-adoption-strategies-across-aws-regions/) | [Share](https://aws.amazon.com/vi/blogs/compute/implementing-advanced-aws-graviton-adoption-strategies-across-aws-regions/ )

Implementing Advanced AWS Graviton Adoption Strategies Across AWS Regions by Matt Howard on 26 AUG 2025 in Advanced (300), Amazon EC2, Best Practices, Graviton Permalink Share

[AWS Graviton Processors](https://aws.amazon.com/ec2/graviton/) can deliver cost savings, improved performance, and reduced carbon footprint when using [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2/) instances. When scaling Graviton deployments across multiple [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/), careful planning helps you consider regional instance type availability factors and optimize capacity. This article explains how to implement advanced configuration strategies for Graviton-enabled [EC2 Auto Scaling](https://aws.amazon.com/ec2/autoscaling/) groups across multiple Regions, helping you maximize instance availability, reduce costs, and maintain consistent application performance even in Regions with Graviton instance type constraints.

**Flexible Instance Type Strategies**

One of the most effective strategies for maximizing Graviton availability is to flexibly use a variety of instance types and families. Instance families (such as m7g, c7g, and r7g) group similar instances of different sizes, each offering increasing proportions of vCPU and memory. When configuring EC2 Auto Scaling groups, try to use at least 10 instance types rather than limiting yourself to just one or two specific types. EC2 Auto Scaling supports this flexibility through a [mixed instance group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/mixed-instances-groups-set-up-overview.html), which allows you to specify multiple instance types in the same group. See the example [AWS CloudFormation](https://aws.amazon.com/cloudformation/) snippet for the EC2 Auto Scaling group [MixedInstancesPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-resource-autoscaling-autoscalinggroup.html cfn-autoscaling-autoscalinggroup-mixedinstancespolicy), which specifies two Graviton instance types belonging to two different families:

"MixedInstancesPolicy": {

"Overrides": \[

{

"InstanceType": "m7g.large"

},

{

"InstanceType": "c7g.xlarge"

}

\]

}

This limited choice significantly reduces access to available capacity pools. Assuming this workload requires at least 2 vCPUs and 8 GiB of memory, you can add the following eight additional Graviton instance types: m6g.large, m8g.large, m6gd.large, m7gd.large, m8gd.large, c6g.xlarge, c6gd.xlarge, and c8g.xlarge. This helps you meet the recommendation of scaling to 10 instance types. While some of these instance types have different prices, you can manage these cost impacts through allocation strategies discussed later in the article.

To efficiently identify all compatible Graviton instance types for your workload, you can use [GetInstanceTypesFromInstanceRequirements](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_GetInstanceTypesFromInstanceRequirements.html). This approach eliminates the manual effort of researching and selecting each individual instance type.

aws ec2 get-instance-types-from-instance-requirements \\
\--architecture-types arm64 \\
\--virtualization-types hvm \\
\--instance-requirements '{"VCpuCount": {"Min": 2,"Max":8}, "MemoryMiB": {"Min": 8000}, "InstanceGenerations":\["current"\]}' \\
\--region us-east-1

This example command returns dozens of compatible Graviton instance types from various families (c7g, c7gd, c7gn, m7g, m7gd, etc.), thereby expanding your capacity options. An EC2 Auto Scaling group's mixed instance policy can allow [up to 40 instance types](https://docs.aws.amazon.com/autoscaling/ec2/APIReference/API_LaunchTemplateOverrides.html API_LaunchTemplateOverrides_Contents), giving you even more flexibility.

After expanding your instance type choices, you need to configure how EC2 Auto Scaling chooses between available instance types. The [OnDemandAllocationStrategy](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-autoscaling-autoscalinggroup-instancesdistribution.html cfn-autoscaling-autoscalingggroup-instancesdistribution-ondemandallocationstrategy) in CloudFormation controls this behavior, providing two approaches: “lowest-price” and “prioritized”. With the “lowest-price” strategy, EC2 Auto Scaling will launch instances from the lowest-priced capacity pool available:

"OnDemandAllocationStrategy": "lowest-price"

This strategy helps manage costs when you have included multiple instance types. Even with increased instance type flexibility, your workloads will automatically choose the most cost-effective option from the available capacity pools. Alternatively, you can use the “prioritized” strategy if you want more control over which instance types are selected first:

"OnDemandAllocationStrategy": "prioritized"

**Regional adaptation techniques**

Not all AWS Regions have the same Graviton instance types available. Differences in instance type availability between regions create challenges when deploying applications consistently across multiple AWS Regions. To address these differences, extend instance type flexibility beyond the minimum of 10 types, ensuring there are enough options in each AWS Region you operate.

To implement this flexibility across AWS Regions, you need to determine which Graviton instance types are available in each target region. AWS provides multiple methods to access this information: check the [Amazon EC2 Instance Types by Region](https://docs.aws.amazon.com/ec2/latest/instancetypes/ec2-instance-regions.html) documentation for a complete list, use the [DescribeInstanceTypeOfferings](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInstanceTypeOfferings.html) Amazon EC2 API to determine the available types programmatically, or visit the [EC2 Instance Types page in the AWS Management Console](https://console.aws.amazon.com/ec2/home InstanceTypes:v=3).

You can also run the GetInstanceTypesFromInstanceRequirements API on different AWS Regions to understand regional differences. For example, running the same queries in US East (N. Virginia) and Asia Pacific (Taipei) shows a significant difference: over 70 compatible instance types in US East (N. Virginia) and 27 in Asia Pacific (Taipei).

\ Query for US East (N. Virginia)
aws ec2 get-instance-types-from-instance-requirements \\
\--architecture-types arm64 \\
\--virtualization-types hvm \\
\--instance-requirements '{"VCpuCount": {"Min": 2,"Max":8}, "MemoryMiB": {"Min": 8000}, "InstanceGenerations":\["current"\]}' \\
\--region us-east-1

\ Query for Asia Pacific (Taipei)
aws ec2 get-instance-types-from-instance-requirements \\
\--architecture-types arm64 \\
\--virtualization-types hvm \\
\--instance-requirements '{"VCpuCount": {"Min": 2,"Max":8}, "MemoryMiB": {"Min": 8000}, "InstanceGenerations":\["current"\]}' \\
\--region ap-east-2

When operating across multiple AWS Regions, design a single mixed instance policy that works across all regions by including instance types that are available across all AWS Regions you operate in. Based on the previous query, you can include the following 10 instance types that are available across both AWS Regions: m6g.large, m7g.large, m6gd.large, m7gd.large, c6g.xlarge, c7g.xlarge, m6g.xlarge, m7g.xlarge, c6gn.xlarge, and m6gd.xlarge.

You should also deploy your EC2 Auto Scaling group across multiple Availability Zones (AZs) for increased fault tolerance and access to deeper capacity pools. To determine which AZs are available in your AWS Region, refer to the Availability Zones documentation or check the Amazon Virtual Private Cloud (Amazon VPC) to determine which AZs are being used by subnets using the Amazon EC2 API. Configure the EC2 Auto Scaling group to use all available AZs using the [AvailabilityZones](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-resource-autoscaling-autoscalinggroup.html cfn-autoscaling-autoscalinggroup-availabilityzones) parameter in CloudFormation AWS::AutoScaling::AutoScalingGroup:

"AvailabilityZones": \[
"us-west-2a",
"us-west-2b",
"us-west-2c",
"us-west-2d",
\]

**Best Practices for Using EC2 Spot Instances with Graviton-Based Instances**

While optimizing regional availability and AZ allocation provides a solid foundation, enhancing your Graviton deployment strategy with configuration [Amazon EC2 Spot](https://aws.amazon.com/ec2/spot/) Instances can significantly improve cost efficiency without sacrificing reliability. When using Spot Instances with Graviton, you should implement strategies that maximize your chances of acquiring and maintaining capacity.

First, [Spot Instance Advisor](https://aws.amazon.com/ec2/spot/instance-advisor/) provides useful information about the frequency of interruptions of different instance types on AWS Regions. Use this tool to identify Graviton instance types with lower interruption rates in your target regions. Then, expand your mixed instance group to include these instance types. Especially for workloads using Spot Instances, maximize instance type flexibility by specifying up to a limit of 40 instance types for EC2 Auto Scaling groups mixed instance policies. This broad selection increases your chances of finding available Spot Instances capacity.

In addition to instance type selection, the allocation strategy you choose significantly affects your ability to maintain Spot Instances capacity. Configure the Spot allocation strategy using the [AWS::AutoScaling::AutoScalingGroup InstancesDistribution](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-autoscaling-autoscalinggroup-instancesdistribution.html) property with parameters [SpotAllocationStrategy](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-autoscaling-autoscalinggroup-instancesdistribution.html cfn-autoscaling-autoscalinggroup-instancesdistribution-spotallocationstrategy) set is[price-capacity-optimized](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-allocation-strategy.html ec2-fleet-allocation-strategies-for-spot-instances), to select Spot pools with the lowest risk of disruption while still considering price:

"InstancesDistribution": {
"SpotAllocationStrategy": "price-capacity-optimized"
}

For workloads that can benefit from more time than the standard two-minute Spot disruption notification, enable [Capacity Rebalancing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-capacity-rebalance.html). This feature, configured via the [AWS::AutoScaling::AutoScalingGroup CapacityRebalance](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-resource-autoscaling-autoscalinggroup.html cfn-autoscaling-autoscalinggroup-capacityrebalance) property, enables EC2 Auto Scaling to proactively respond to rebalancing recommendations by launching a new Spot Instance two minutes before the running instance receives a Spot interruption notification, thus providing additional time to smoothly transition:

"CapacityRebalance": true

For maximum flexibility and better capacity access, consider combining both **x86** and **ARM** architectures in **launch templates**. While **Graviton capacity pools** are newer and sometimes smaller than x86, the hybrid architecture approach ensures you can still launch instances even if one architecture is limited. For detailed instructions, see the AWS article: [Supporting AWS Graviton2 and x86 instance types in the same Auto Scaling group](https://aws.amazon.com/blogs/compute/supporting-aws-graviton2-and-x86-instance-types-in-the-same-auto-scaling-group/).

**Attribute-based instance type selection**

While mixed instance policies with a list of specific instance types provide great flexibility, AWS also provides a more powerful method for dynamically selecting instance types: [attribute-based instance type selection](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-attribute-based-instance-type-selection.html). This method makes management easier by allowing you to specify the attributes your application needs instead of specific instance types, automatically adapting to new instance types, and handling regional availability differences.

You can implement property-based instance type selection in the EC2 Launch Template via the [AWS::EC2::LaunchTemplate InstanceRequirements] attribute(https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-ec2-launchtemplate-instancerequirements.html):

{ 

"InstanceRequirements": { 

"AcceleratorCount": { 

"Max": 0 

}, 

"BareMetal": "excluded", 

"BaselinePerformanceFactors": { 

"Cpu": { 

"References": \[ 

{ 

"InstanceFamily": "c7g" 

} 

\] 

} 

}, 

"InstanceGenerations": \[ 

"current"

\],

"MemoryMiB": {

"Min": 8000

},

"VCpuCount": {

"Min": 4

}

}

}

[BaselinePerformanceFactors](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-ec2-launchtemplate-baselineperformancefactors.html) in AWS::EC2::LaunchTemplate InstanceRequirements ensures [performance protection](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-attribute-based-instance-type-selection.html ec2fleet-abis-performance-protection). This feature ensures that EC2 Auto Scaling groups use instance types that meet or exceed the defined baseline performance. When you specify an instance family like “c7g” as the baseline reference, Amazon EC2 automatically excludes instance types below this performance level, even if they match the other attributes specified. With Graviton deployments, specifying “c7g” ensures onlyselect instance types that have equivalent or better performance than Graviton3 processors.

Property-based instance type selection also allows specifying instance types in the template that may not be available in an AWS Region by using [AllowedInstanceTypes](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-ec2-launchtemplate-instancerequirements.html cfn-ec2-launchtemplate-instancerequirements-allowedinstancetypes):

{

"AllowedInstanceTypes": \[

"m6g.large",

"m7g.large",

"m8g.large"

\]

}

This approach helps EC2 Auto Scaling groups use new instance types when available and deploy them automatically in other AWS Regions as they become available. This single template simplifies the deployment and management of instance selection in EC2 Auto Scaling groups across multiple regions.

**Special Notes**

The following special considerations should be noted.

**Performance Testing with Multiple Instance Types**

When deploying instance type flexibility, a common concern is that all instance types need to be tested with the application. Testing 40 different instance types is impractical for most organizations. Instead, consider the following approaches to reduce the amount of testing while still ensuring performance:

1. Graviton instance families within the same generation (e.g., c7g, m7g, r7g) use the same processor, providing similar performance. Therefore, you can include multiple instance types from the same generation when testing a representative instance.

2. Consider including variants within the family (e.g., c7gd with NVMe storage), as they provide specialized capabilities without changing the underlying CPU architecture.

3. For maximum flexibility, include multiple instance generations.

If an application runs well on Graviton3, it will most likely run better on Graviton4, allowing you to specify both in an EC2 Auto Scaling group.

**Reserving a Specific Graviton Type**

If a workload requires a specific Graviton instance type, use [EC2 Capacity Reservations](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-capacity-reservations.html), which allows you to reserve capacity for EC2 instances in a specific AZ for any period of time.

* On-Demand Capacity Reservations (ODCR) are for immediate use and do not require a term commitment.

* Future-dated Capacity Reservations allow you to specify when capacity needs to be available along with a commitment period.

**Amazon EMR workloads**

Although [Amazon EMR](https://aws.amazon.com/emr/) clusters exist only in a single AZ, you can use Amazon EMR instance fleets to select multiple subnets across different AZs. When you initialize a cluster, Amazon EMR searches across these subnets for specific instances and purchasing methods, thereby accessing a deeper capacity pool. With [Instance Fleets](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-instance-fleet.html), you can assign up to 30 EC2 instance types to each primary, core, and task node group, significantly improving instance flexibility and availability. See also: [Responding to Amazon EMR cluster insufficient instance capacity events](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-events-response-insuff-capacity.html).

**Conclusion**

This article presents advanced strategies for maximizing AWS Graviton adoption across multiple AWS Regions. You can use the provided AWS CloudFormation examples as templates for your own deployments. Following these practices helps maintain consistent application performance and maximize Graviton instance availability across all AWS Regions you operate, even as Graviton availability continues to scale across AWS's global infrastructure. For a comprehensive guide to maximizing Graviton deployments, see the [AWS Graviton Technical Guide](https://github.com/aws/aws-graviton-getting-started).

**Source:[https://aws.amazon.com/vi/blogs/compute/implementing-advanced-aws-graviton-adoption-strategies-across-aws-regions/](https://aws.amazon.com/vi/blogs/compute/implementing-advanced-aws-graviton-adoption-strategies-across-aws-regions/)**
