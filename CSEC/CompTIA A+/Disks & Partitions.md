# Partitioning Schemes

Indicates come Partitioning properties like size and number of partitions

## MBR: Master Boot Record

- Creates a table that contains a Map of Partitions and is saved in the 1st sector in the disk
- The most common partitioning system
- Required for 32-bit, legacy BIOS, UEFI in CSM mode
- Maximum size of disk is 2TB ie. the maximum size of a partition is 2TB
- Maximum Number of Partitions: 4

### MBR partitions types

Primary

- Must be Used

Extended

- Optional, mostly used to add 5th disk

## GPT: Global Partition Table

- A maximum theoretical Partition size limit of 9.4 Zettabytes and actual of 256TB
- A maximum partitions number of 128, ie Extended partitioning is not needed
- Any Linux can boot from a GPT. but, only 64-bit win + native (non CSM) UEFI can boot from a GPT