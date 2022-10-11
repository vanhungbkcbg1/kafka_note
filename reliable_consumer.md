### minimum in-sync replicas
can config gia tri nay de make sure data duoc sync toi it nhat 2 replicas de make sure availability, neu trong qua trinh khi
so luong replicas ko du thi se throw exception

If you would like to be sure that committed data is written to more than one replica,
you need to set the minimum number of in-sync replicas to a higher value. If a topic
has three replicas and you set min.insync.replicas to 2 , then you can only write to
a partition in the topic if at least two out of the three replicas are in-sync

When all three replicas are in-sync, everything proceeds normally. This is also true if
one of the replicas becomes unavailable. However, if two out of three replicas are not
available, the brokers will no longer accept produce requests. Instead, producers that
attempt to send data will receive NotEnoughReplicasException . Consumers can con‐
tinue reading existing data. In effect, with this configuation, a single in-sync replica
becomes read-only. This prevents the undesirable situation where data is produced
and consumed, only to disappear when unclean election occurs. In order to recover
from this read-only situation, we must make one of the two unavailable partitions
available again (maybe restart the broker) and wait for it to catch up and get in-sync
