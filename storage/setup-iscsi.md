# How to setup iscsi storage from external storage to solaris 11

- Check current initiator 
```
# iscsiadm list initiator-node
```
- Make discovery method static.
```
# iscsiadm modify discovery --static enable
```
- Make sure iSCSI storage can be connected
```
# ping 10.128.110.101
10.128.110.101 is alive
```
- Discover the targets.
```
# iscsiadm add discovery-address 10.128.110.101:3260
```
- List the discovery result.
```
# iscsiadm list discovery-address -v 10.128.110.101
Discovery Address: 10.128.110.101:3260
        Target name: iqn.2005-10.org.freenas.ctl:asm-t1
                Target address:  10.128.110.101:3260, 65535
```
- Add discovered targets to discovery table.
```
# iscsiadm add static-config iqn.2005-10.org.freenas.ctl:asm-t1,10.128.110.101
```
- List the details of a specific target.
```
# iscsiadm list target -S iqn.2005-10.org.freenas.ctl:asm-t1
```
