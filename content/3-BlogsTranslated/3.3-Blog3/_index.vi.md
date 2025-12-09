---
title: "Triển khai các chiến lược áp dụng AWS Graviton nâng cao trên các AWS Regions"
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

**Triển khai các chiến lược áp dụng AWS Graviton nâng cao trên các AWS Regions**

  Bởi Matt Howard | vào ngày 26 tháng 8 năm 2025 | trong [Advanced (300)](https://aws.amazon.com/blogs/compute/category/learning-levels/advanced-300/), [Amazon EC2](https://aws.amazon.com/blogs/compute/category/compute/amazon-ec2/), [Best Practices](https://aws.amazon.com/blogs/compute/category/post-types/best-practices/), [Graviton](https://aws.amazon.com/blogs/compute/category/compute/graviton/) | [Permalink](https://aws.amazon.com/blogs/compute/implementing-advanced-aws-graviton-adoption-strategies-across-aws-regions/) | [Share](https://aws.amazon.com/vi/blogs/compute/implementing-advanced-aws-graviton-adoption-strategies-across-aws-regions/ )

Triển khai các chiến lược áp dụng AWS Graviton nâng cao trên các AWS Regions bởi Matt Howard vào ngày 26 AUG 2025 trong Advanced (300), Amazon EC2, Best Practices, Graviton Permalink Share

[AWS Graviton Processors](https://aws.amazon.com/ec2/graviton/) có thể mang lại tiết kiệm chi phí, cải thiện hiệu suất và giảm lượng khí thải carbon khi sử dụng các [Amazon Elastic Compute Cloud (Amazon EC2)](https://aws.amazon.com/ec2/) instances. Khi mở rộng triển khai Graviton trên nhiều [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/), việc lập kế hoạch cẩn thận sẽ giúp bạn cân nhắc các yếu tố về khả năng sẵn có của loại instance theo từng vùng và tối ưu hóa năng lực. Bài viết này hướng dẫn cách triển khai các chiến lược cấu hình nâng cao cho các Graviton-enabled [EC2 Auto Scaling](https://aws.amazon.com/ec2/autoscaling/) groups trên nhiều Regions, giúp bạn tối đa hóa khả năng sẵn có của instance, giảm chi phí và duy trì hiệu suất ứng dụng nhất quán ngay cả ở các Regions có hạn chế về loại instance Graviton.

**Chiến lược linh hoạt loại instance** 

Một trong những chiến lược hiệu quả nhất để tối đa hóa khả năng sẵn có của Graviton là linh hoạt sử dụng nhiều loại instance và family khác nhau. Instance families (như m7g, c7g, và r7g) nhóm các instance tương tự với các kích thước khác nhau, mỗi kích thước cung cấp tỉ lệ vCPU và bộ nhớ tăng dần. Khi cấu hình EC2 Auto Scaling groups, hãy cố gắng sử dụng ít nhất 10 loại instance thay vì giới hạn chỉ một hoặc hai loại cụ thể. EC2 Auto Scaling hỗ trợ sự linh hoạt này thông qua [mixed instances group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/mixed-instances-groups-set-up-overview.html), cho phép bạn chỉ định nhiều loại instance trong cùng một group. Hãy xem ví dụ snippet [AWS CloudFormation](https://aws.amazon.com/cloudformation/) cho EC2 Auto Scaling group [MixedInstancesPolicy](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-resource-autoscaling-autoscalinggroup.html cfn-autoscaling-autoscalinggroup-mixedinstancespolicy), trong đó chỉ định hai loại Graviton instance thuộc hai family khác nhau:

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

Việc giới hạn lựa chọn này làm giảm đáng kể khả năng truy cập vào các capacity pools sẵn có. Giả sử workload này cần tối thiểu 2 vCPU và 8 GiB bộ nhớ, bạn có thể thêm tám loại Graviton instance bổ sung sau: m6g.large, m8g.large, m6gd.large, m7gd.large, m8gd.large, c6g.xlarge, c6gd.xlarge và c8g.xlarge. Điều này giúp bạn đáp ứng khuyến nghị về việc linh hoạt sử dụng 10 loại instance. Mặc dù một số loại instance này có mức giá khác nhau, bạn có thể quản lý các tác động về chi phí này thông qua các chiến lược phân bổ được thảo luận sau trong bài viết.

Để xác định hiệu quả tất cả các loại Graviton instance tương thích cho workload của bạn, bạn có thể sử dụng [GetInstanceTypesFromInstanceRequirements](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_GetInstanceTypesFromInstanceRequirements.html). Cách tiếp cận này loại bỏ nỗ lực thủ công trong việc nghiên cứu và chọn từng loại instance riêng lẻ.

aws ec2 get-instance-types-from-instance-requirements \\  
\--architecture-types arm64 \\  
\--virtualization-types hvm \\  
\--instance-requirements '{"VCpuCount": {"Min": 2,"Max":8}, "MemoryMiB": {"Min": 8000}, "InstanceGenerations":\["current"\]}' \\  
\--region us-east-1

Lệnh ví dụ này trả về hàng chục loại Graviton instance tương thích thuộc nhiều family khác nhau (c7g, c7gd, c7gn, m7g, m7gd, v.v.), từ đó mở rộng các tùy chọn capacity của bạn. Mixed instance policy của một EC2 Auto Scaling group có thể cho phép [tối đa 40 loại phiên bản](https://docs.aws.amazon.com/autoscaling/ec2/APIReference/API_LaunchTemplateOverrides.html API_LaunchTemplateOverrides_Contents), nhờ đó bạn có nhiều không gian linh hoạt hơn nữa.

Sau khi mở rộng lựa chọn loại instance, bạn cần cấu hình cách EC2 Auto Scaling chọn giữa các loại instance sẵn có. Thuộc tính [OnDemandAllocationStrategy](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-autoscaling-autoscalinggroup-instancesdistribution.html cfn-autoscaling-autoscalinggroup-instancesdistribution-ondemandallocationstrategy) trong CloudFormation kiểm soát hành vi này, cung cấp hai cách tiếp cận: “lowest-price” và “prioritized”. Với chiến lược “lowest-price”, EC2 Auto Scaling sẽ khởi chạy các instance từ capacity pool có giá thấp nhất sẵn có:

"OnDemandAllocationStrategy": "lowest-price"

Chiến lược này giúp quản lý chi phí khi bạn đã bao gồm nhiều loại instance khác nhau. Ngay cả khi đã mở rộng tính linh hoạt về loại instance, workloads của bạn sẽ tự động chọn phương án tiết kiệm chi phí nhất từ các **capacity pools** sẵn có. Ngoài ra, bạn có thể sử dụng chiến lược “prioritized” khi muốn kiểm soát nhiều hơn về loại instance nào được chọn trước:

"OnDemandAllocationStrategy": "prioritized"

**Kỹ thuật thích ứng theo vùng (Regional adaptation techniques)** 

Không phải tất cả các AWS Regions đều có sẵn cùng loại Graviton instance. Sự khác biệt về khả năng sẵn có của loại instance giữa các vùng tạo ra thách thức khi triển khai ứng dụng một cách nhất quán trên nhiều AWS Regions. Để xử lý những khác biệt này, hãy mở rộng tính linh hoạt về loại instance vượt quá tối thiểu 10 loại, đảm bảo có đủ tùy chọn trong mỗi AWS Region mà bạn vận hành.

Để triển khai tính linh hoạt này trên các AWS Regions, bạn cần xác định loại Graviton instance nào có sẵn ở từng vùng mục tiêu. AWS cung cấp nhiều phương pháp để truy cập thông tin này: kiểm tra tài liệu [Amazon EC2 Instance Types by Region](https://docs.aws.amazon.com/ec2/latest/instancetypes/ec2-instance-regions.html) để có danh sách đầy đủ, sử dụng [DescribeInstanceTypeOfferings](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeInstanceTypeOfferings.html) Amazon EC2 API để xác định các loại có sẵn theo lập trình, hoặc truy cập trang [EC2 Instance Types page in the AWS Management Console](https://console.aws.amazon.com/ec2/home InstanceTypes:v=3).

Bạn cũng có thể chạy GetInstanceTypesFromInstanceRequirements API trên các AWS Regions khác nhau để hiểu sự khác biệt theo vùng. Ví dụ, chạy các truy vấn giống nhau ở US East (N. Virginia) và Asia Pacific (Taipei) cho thấy sự khác biệt đáng kể: hơn 70 loại instance tương thích ở US East (N. Virginia) và 27 loại ở Asia Pacific (Taipei).

\  Query for US East (N. Virginia)  
aws ec2 get-instance-types-from-instance-requirements \\  
\--architecture-types arm64 \\  
\--virtualization-types hvm \\  
\--instance-requirements '{"VCpuCount": {"Min": 2,"Max":8}, "MemoryMiB": {"Min": 8000}, "InstanceGenerations":\["current"\]}' \\  
\--region us-east-1

\  Query for Asia Pacific (Taipei)  
aws ec2 get-instance-types-from-instance-requirements \\  
\--architecture-types arm64 \\  
\--virtualization-types hvm \\  
\--instance-requirements '{"VCpuCount": {"Min": 2,"Max":8}, "MemoryMiB": {"Min": 8000}, "InstanceGenerations":\["current"\]}' \\  
\--region ap-east-2

Khi vận hành trên nhiều AWS Regions, hãy thiết kế một mixed instance policy duy nhất hoạt động ở tất cả các vùng bằng cách bao gồm các loại instance có sẵn ở tất cả các AWS Regions mà bạn đang hoạt động. Dựa trên kết quả truy vấn trước, bạn có thể bao gồm 10 loại instance sau có sẵn ở cả hai AWS Regions: m6g.large, m7g.large, m6gd.large, m7gd.large, c6g.xlarge, c7g.xlarge, m6g.xlarge, m7g.xlarge, c6gn.xlarge và m6gd.xlarge.

Bạn cũng nên triển khai EC2 Auto Scaling group của mình trên nhiều Availability Zones (AZs) để tăng khả năng chịu lỗi và truy cập vào các capacity pools sâu hơn. Để xác định các AZ có sẵn trong AWS Region của bạn, tham khảo tài liệu [Availability Zones](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-availability-zones.html) hoặc kiểm tra [Amazon Virtual Private Cloud (Amazon VPC)](https://aws.amazon.com/vpc/) để xác định AZ nào đang được các subnet sử dụng thông qua [DescribeSubnets](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeSubnets.html) Amazon EC2 API. Cấu hình EC2 Auto Scaling group để sử dụng tất cả các AZ có sẵn bằng cách sử dụng tham số [AvailabilityZones](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-resource-autoscaling-autoscalinggroup.html cfn-autoscaling-autoscalinggroup-availabilityzones) trong CloudFormation AWS::AutoScaling::AutoScalingGroup:

"AvailabilityZones": \[  
  "us-west-2a",  
  "us-west-2b",  
  "us-west-2c",  
  "us-west-2d",  
\]

**Các phương pháp hay nhất để sử dụng EC2 Spot Instances với các phiên bản dựa trên Graviton**

Mặc dù tối ưu hóa khả năng sẵn có theo vùng và phân bổ AZ cung cấp nền tảng vững chắc, việc nâng cao chiến lược triển khai Graviton với cấu hình [Amazon EC2 Spot](https://aws.amazon.com/ec2/spot/) Instances đúng cách có thể cải thiện đáng kể hiệu quả chi phí mà không làm giảm độ tin cậy. Khi sử dụng Spot Instances với Graviton, bạn nên triển khai các chiến lược tối đa hóa cơ hội có được và duy trì capacity.

Đầu tiên, [Spot Instance Advisor](https://aws.amazon.com/ec2/spot/instance-advisor/) cung cấp thông tin hữu ích về tần suất gián đoạn của các loại instance khác nhau trên các AWS Regions. Sử dụng công cụ này để xác định các loại Graviton instance có tỉ lệ gián đoạn thấp hơn trong các vùng mục tiêu của bạn. Sau đó, mở rộng mixed instance group để bao gồm các loại instance này. Đặc biệt với workload sử dụng Spot Instances, hãy tối đa hóa tính linh hoạt về loại instance bằng cách chỉ định tối đa giới hạn 40 loại instance cho EC2 Auto Scaling groups mixed instance policies. Việc lựa chọn rộng rãi này tăng cơ hội tìm được Spot Instances capacity sẵn có.

Ngoài việc chọn loại instance, chiến lược phân bổ mà bạn chọn ảnh hưởng đáng kể đến khả năng duy trì Spot Instances capacity. Cấu hình chiến lược phân bổ Spot bằng cách sử dụng thuộc tính [AWS::AutoScaling::AutoScalingGroup InstancesDistribution](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-autoscaling-autoscalinggroup-instancesdistribution.html) với tham số [SpotAllocationStrategy](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-autoscaling-autoscalinggroup-instancesdistribution.html cfn-autoscaling-autoscalinggroup-instancesdistribution-spotallocationstrategy) đặt là[price-capacity-optimized](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-allocation-strategy.html ec2-fleet-allocation-strategies-for-spot-instances), để chọn các Spot pools có nguy cơ gián đoạn thấp nhất đồng thời vẫn cân nhắc giá:

"InstancesDistribution": {  
  "SpotAllocationStrategy": "price-capacity-optimized"  
}

Đối với các workload có thể hưởng lợi từ thời gian nhiều hơn so với thông báo gián đoạn Spot chuẩn hai phút, hãy bật [Capacity Rebalancing](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-capacity-rebalance.html). Tính năng này, được cấu hình thông qua thuộc tính [AWS::AutoScaling::AutoScalingGroup CapacityRebalance](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-resource-autoscaling-autoscalinggroup.html cfn-autoscaling-autoscalinggroup-capacityrebalance), cho phép EC2 Auto Scaling phản ứng chủ động theo các khuyến nghị rebalancing bằng cách khởi chạy một Spot Instance mới trước khi instance đang chạy nhận thông báo gián đoạn Spot hai phút, từ đó cung cấp thêm thời gian để thực hiện chuyển đổi một cách mượt mà:

"CapacityRebalance": true

Để đạt tính linh hoạt tối đa và truy cập capacity tốt hơn, hãy xem xét việc kết hợp cả kiến trúc **x86** và **ARM** trong **launch templates**. Mặc dù các **Graviton capacity pools** mới hơn và đôi khi nhỏ hơn so với x86, cách tiếp cận kiến trúc hỗn hợp đảm bảo bạn vẫn có thể khởi chạy instance ngay cả khi một kiến trúc có sẵn hạn chế. Để hướng dẫn chi tiết, tham khảo bài viết AWS:[Supporting AWS Graviton2 and x86 instance types in the same Auto Scaling group](https://aws.amazon.com/blogs/compute/supporting-aws-graviton2-and-x86-instance-types-in-the-same-auto-scaling-group/).

**Lựa chọn loại instance dựa trên thuộc tính (Attribute-based instance type selection)**

Mặc dù mixed instance policies với danh sách loại instance cụ thể cung cấp sự linh hoạt tuyệt vời, AWS còn cung cấp một phương pháp mạnh mẽ hơn cho việc lựa chọn động loại instance: [attribute-based instance type selection](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-attribute-based-instance-type-selection.html). Phương pháp này giúp quản lý dễ dàng hơn bằng cách cho phép bạn chỉ định các thuộc tính mà ứng dụng cần thay vì loại instance cụ thể, tự động thích ứng với các loại instance mới và xử lý sự khác biệt về sẵn có theo vùng.

Bạn có thể triển khai lựa chọn loại instance dựa trên thuộc tính trong EC2 Launch Template thông qua thuộc tính [AWS::EC2::LaunchTemplate InstanceRequirements](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-ec2-launchtemplate-instancerequirements.html):

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

[BaselinePerformanceFactors](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-ec2-launchtemplate-baselineperformancefactors.html) trong AWS::EC2::LaunchTemplate InstanceRequirements đảm bảo [performance protection](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-fleet-attribute-based-instance-type-selection.html ec2fleet-abis-performance-protection). Tính năng này đảm bảo EC2 Auto Scaling group sử dụng các loại instance đạt hoặc vượt mức hiệu suất cơ bản đã định. Khi bạn chỉ định một instance family như “c7g” làm tham chiếu cơ sở, Amazon EC2 sẽ tự động loại trừ các loại instance dưới mức hiệu suất này, ngay cả khi chúng phù hợp với các thuộc tính khác đã chỉ định. Với triển khai Graviton, việc chỉ định “c7g” đảm bảo chỉ chọn các loại instance có hiệu suất tương đương hoặc tốt hơn Graviton3 processors.

Lựa chọn loại instance dựa trên thuộc tính cũng cho phép chỉ định các loại instance trong template mà có thể chưa có sẵn trong một AWS Region bằng cách sử dụng [AllowedInstanceTypes](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-properties-ec2-launchtemplate-instancerequirements.html cfn-ec2-launchtemplate-instancerequirements-allowedinstancetypes):

{

  "AllowedInstanceTypes": \[

    "m6g.large",

    "m7g.large",

    "m8g.large"

  \]

}

Cách tiếp cận này giúp EC2 Auto Scaling group sử dụng các loại instance mới khi có sẵn và triển khai tự động ở các AWS Regions khác khi chúng trở nên khả dụng. Template duy nhất này đơn giản hóa việc triển khai và quản lý lựa chọn instance trong EC2 Auto Scaling groups trên nhiều vùng.

**Các lưu ý đặc biệt**

Những cân nhắc đặc biệt sau đây cần được lưu ý.

**Kiểm thử hiệu suất với nhiều loại instance**

Khi triển khai linh hoạt loại instance, một mối quan tâm phổ biến là cần kiểm thử tất cả các loại instance với ứng dụng. Việc thử nghiệm 40 loại instance khác nhau là không thực tế đối với hầu hết tổ chức. Thay vào đó, hãy cân nhắc các cách tiếp cận sau để giảm khối lượng kiểm thử mà vẫn đảm bảo hiệu suất:

1. Các Graviton instance families trong cùng thế hệ (ví dụ: c7g, m7g, r7g) sử dụng cùng một processor, cung cấp hiệu suất tương tự. Do đó, bạn có thể bao gồm nhiều loại instance từ cùng thế hệ sau khi kiểm thử một instance đại diện.

2. Cân nhắc bao gồm các biến thể trong family (ví dụ: c7gd với NVMe storage), vì chúng cung cấp khả năng chuyên biệt mà không thay đổi kiến trúc CPU cơ bản.

3. Để đạt tính linh hoạt tối đa, hãy bao gồm nhiều thế hệ instance. 

Nếu ứng dụng chạy tốt trên Graviton3, thì rất có thể sẽ chạy tốt hơn trên Graviton4, cho phép bạn chỉ định cả hai trong EC2 Auto Scaling group.

**Đặt trước loại Graviton cụ thể**

Nếu workload cần một loại Graviton instance cụ thể, hãy sử dụng [EC2 Capacity Reservations](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-capacity-reservations.html), cho phép đặt trước capacity cho EC2 instance trong một AZ cụ thể trong bất kỳ khoảng thời gian nào.

* On-Demand Capacity Reservations (ODCR) dành cho sử dụng ngay và không yêu cầu cam kết thời hạn.

* Future-dated Capacity Reservations cho phép chỉ định thời điểm capacity cần sẵn có cùng với thời gian cam kết.

   **Amazon EMR workloads**

   Mặc dù các [Amazon EMR](https://aws.amazon.com/emr/) clusters chỉ tồn tại trong một AZ, bạn có thể sử dụng Amazon EMR instance fleets để chọn nhiều subnet qua các AZ khác nhau. Khi khởi tạo cluster, Amazon EMR tìm kiếm qua các subnet này để tìm instance và phương thức mua cụ thể, từ đó truy cập vào capacity pool sâu hơn. Với [Instance Fleets](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-instance-fleet.html), bạn có thể chỉ định tới 30 loại EC2 instance cho mỗi nhóm node primary, core, và task, cải thiện đáng kể tính linh hoạt và khả năng sẵn có của instance. Tham khảo thêm: [Responding to Amazon EMR cluster insufficient instance capacity events](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-events-response-insuff-capacity.html).

**Kết luận**

Bài viết này trình bày các chiến lược nâng cao để tối đa hóa việc áp dụng AWS Graviton trên nhiều AWS Regions. Bạn có thể sử dụng các ví dụ AWS CloudFormation được cung cấp như template cho triển khai của riêng mình. Theo các phương pháp này giúp duy trì hiệu suất ứng dụng nhất quán và tối đa hóa khả năng sẵn có của Graviton instance trên tất cả các AWS Regions mà bạn vận hành, ngay cả khi khả năng sẵn có của Graviton tiếp tục mở rộng trên hạ tầng toàn cầu của AWS. Để có hướng dẫn toàn diện về tối đa hóa triển khai Graviton, hãy tham khảo [AWS Graviton Technical Guide](https://github.com/aws/aws-graviton-getting-started).

**Nguồn:[https://aws.amazon.com/vi/blogs/compute/implementing-advanced-aws-graviton-adoption-strategies-across-aws-regions/](https://aws.amazon.com/vi/blogs/compute/implementing-advanced-aws-graviton-adoption-strategies-across-aws-regions/)**



