# Intel HPC Platform Specification<a name="intel-hpc-platform-specification"></a>

AWS ParallelCluster is compliant with the Intel HPC Platform Specification\. The Intel HPC Platform Specification provides a set of compute, fabric, memory, storage, and software requirements to ensure a high standard of quality and compatibility with HPC workloads\.

To be compliant with the Intel HPC Platform Specification, the following requirements must be met:
+ The operating system must be CentOS 7 \(` = centos7`\)\.
+ The instance type for the compute nodes must have an Intel CPU and at least 64 GB of memory\. For the `c5` family of instance types, this means the instance type must be at least a `c5.9xlarge` \(` = c5.9xlarge`\)\.
+ The master node must have at least 200 GB of storage\.
+ The End User License Agreement for Intel Parallel Studio must be accepted \(` = true`\)\.
+ Each compute node must have at least 80 GB of storage \(` = 80`\)\.

The storage can be local or on a network \(NFS shared from the master node, Amazon EBS or Amazon FSx for Lustre\), and it can be shared\.