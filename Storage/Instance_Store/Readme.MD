- An instance store provides temporary (non-persistent) block-level storage for your instance.
- ephemeral storage is also known as instance store.
- This is different to EBS which provides persistent storage but is also a block storage service that can be a root or additional volume.

- Instance store storage is located on disks that are physically attached to the host computer.

- Instance store is ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

- You can specify instance store volumes for an instance only when you launch it.

- You can’t detach an instance store volume from one instance and attach it to a different instance.

- The instance type determines the size of the instance store available, and the type of hardware used for the instance store volumes.

- Instance store volumes are included as part of the instance’s usage cost.

- Some instance types use NVMe or SATA-based solid-state drives (SSD) to deliver high random I/O performance.

- This is a good option when you need storage with very low latency, but you don’t need the data to persist when the instance terminates, or you can take advantage of fault-tolerant architectures.

- EXAM TIP: Instance stores offer very high performance and low latency. If you can afford to lose an instance, i.e. you are replicating your data, these can be a good solution for high performance/low latency requirements. Look out for questions that mention distributed or replicated databases that need high I/O. Also, remember that the cost of instance stores is included in the instance charges so it can also be more cost-effective than EBS Provisioned IOPS.

### EBS vs Instance Store
- EBS-backed means the root volume is an EBS volume and storage is persistent.
- Instance store-backed means the root volume is an instance store volume and storage is not persistent.
- On an EBS-backed instance, the default action is for the root EBS volume to be deleted upon termination.
- Instance store volumes are sometimes called Ephemeral storage (non-persistent).
- Instance store backed instances cannot be stopped. If the underlying host fails the data will be lost.
- Instance store volume root devices are created from AMI templates stored on S3.
- EBS backed instances can be stopped. You will not lose the data on this instance if it is stopped (persistent).
- EBS volumes can be detached and reattached to other EC2 instances.
- EBS volume root devices are launched from AMI’s that are backed by EBS snapshots.
- Instance store volumes cannot be detached/reattached.
- When rebooting the instances for both types data will not be lost.
- By default, both root volumes will be deleted on termination unless you configured otherwise.
