# AWS ParallelCluster Troubleshooting<a name="troubleshooting"></a>

The AWS ParallelCluster community maintains a Wiki with many troubleshooting tips at the [aws\-parallelcluster wiki](https://github.com/aws/aws-parallelcluster/wiki/)\.

## Failure submitting AWS Batch multi\-node parallel jobs<a name="troubleshooting-aws-batch-mnp"></a>

If you have problems submitting multi\-node parallel jobs when using AWS Batch as the job scheduler,we recommend that you upgrade to AWS ParallelCluster 2\.5\.0\. If that is not feasible, you can use a workaround\. For information, see [Self patch a Cluster Used for Submitting Multi node Parallel Jobs through AWS Batch](https://github.com/aws/aws-parallelcluster/wiki/Self-patch-a-Cluster-Used-for-Submitting-Multi-node-Parallel-Jobs-through-AWS-Batch)\.

## Placement Groups and Instance Launch Issues<a name="placement-groups-and-instance-launch-issues"></a>

To get the lowest inter\-node latency, we recommend that you use a *placement group*\. A placement group guarantees that your instances are on the same networking backbone\. If not enough instances are available when the request is made, an `InsufficientInstanceCapacity` error is returned\. To reduce the possibility of receiving an `InsufficientInstanceCapacity` error when using cluster placement groups, set the `` parameter to `DYNAMIC` and set the `` parameter to `compute`\.

If a high performance shared filesystem is needed, consider using [Amazon FSx for Lustre](http://aws.amazon.com/fsx/lustre/)\.

If the master node must be in the placement group, use the same instance type and subnet for both the master and compute nodes\. In other words, the `` parameter has the same value as the `` parameter, the `` parameter is set to `cluster`, and the `` parameter is not specified\. This means that the value of the `` parameter is used for the compute nodes\.

For more information, see [Troubleshooting Instance Launch issues](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/troubleshooting-launch.html) and [Placement Groups Roles and Limitations](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html#concepts-placement-groups) in the *Amazon EC2 User Guide for Linux Instances*

## Directories that cannot be replaced<a name="directories-cannot-be-replaced"></a>

The following directories are shared between the nodes and cannot be replaced\.

`/home`  
This includes the default user home folder \(`/home/ec2_user` on Amazon Linux, `/home/centos` on CentOS, and `/home/ubuntu` on Ubuntu\.\)

`/opt/intel`  
This includes Intel MPI, Intel Parallel Studio, and related files\.

`/opt/sge`  
This includes Son of Grid Engine and related files\. \(Conditional, only if ` = sge`\.\)

`/opt/slurm`  
This includes Slurm Workload Manager and related files\. \(Conditional, only if ` = slurm`\.\)

`/opt/torque`  
This includes Torque Resource Manager and related files\. \(Conditional, only if ` = torque`\.\)

## NICE DCV troubleshooting<a name="nice-dcv-troubleshooting"></a>

The logs for NICE DCV are written to files in the `/var/log/dcv/` directory\. Reviewing these logs can help to troubleshoot problems\.

The instance type should have at least 1\.7 GiB of RAM to run NICE DCV\. Nano and micro instance types do not have enough memory to run NICE DCV\.