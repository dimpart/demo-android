# Secure Chat (Android version)
Demo project of DIM Client, just for study purpose.

Dependencies:

- [DIM SDK (sdk-java)](https://github.com/dimchat/sdk-java)
	- [DIM Core (core-java)](https://github.com/dimchat/core-java)
		- [DaoKeDao (dkd-java)](https://github.com/dimchat/dkd-java)
		- [MingKeMing (mkm-java)](https://github.com/dimchat/mkm-java)
		- [Crypto](https://github.com/dimchat/mkm-java/tree/master/Crypto) digest, coders & keys
- Plugins
	- [Core Plugins](https://github.com/dimchat/plugins-java/tree/master/Plugins)
	- [Crypto Plugins](https://github.com/dimchat/plugins-java/tree/master/CryptoPlugins) - key plugins powered by [bouncy-castle](https://www.bouncycastle.org/)
	- [Native Plugins](https://github.com/dimchat/plugins-java/tree/master/NativePlugins) - key plugins based on JNI
- [Network Module](https://github.com/dimpart/demo-java/tree/master/StarGate)
	- [Star Trek](https://github.com/moky/StarTrek) channel, connection, hub, ...
	- [TCP](https://github.com/moky/wormhole/tree/master/tcp-java)
	- [UDP](https://github.com/moky/wormhole/tree/master/udp-java)
	- [State Machine](https://github.com/moky/FiniteStateMachine/tree/master/fsm-java)
- Demo Libs
	- [Common](https://github.com/dimpart/demo-java/tree/main/Common) - common module for station/client
	- [Network](https://github.com/dimpart/demo-java/tree/main/Network) - network module for station/client
	- [Database](https://github.com/dimpart/demo-java/tree/main/SQLite) - database module powered by [SQLite](https://xerial.org/)
	- [Client](https://github.com/dimpart/demo-java/tree/main/Client) - client module

## Sub Modules

### SDK Modules

|   Module   | Version |  Description     |
|------------|---------|------------------|
| Crypto     | 2.1.0   | Keys             |
| MingKeMing | 2.1.0   | Account Module   |
| DaoKeDao   | 2.1.0   | Message Module   |
| DIMP       | 2.1.0   | Core Protocols   |
| SDK        | 2.1.0   |                  |
| Plugins    | 2.1.0   |                  |

### Network Modules

|   Module   | Version |  Description     |
|------------|---------|------------------|
| ByteArray  | 0.1.2   | Byte Buffer      |
| TLV        | 0.1.4   | Tag Length Value |
| STUN       | 0.1.5   |                  |
| TURN       | 0.1.5   |                  |
| MTP        | 0.1.7   | Network Packing  |
| StarTrek   | 1.1.0   | Transport        |
| TCP        | 1.1.0   |                  |
| UDP        | 1.1.0   |                  |
| DMTP       | 0.2.3   | Binary Messaging |

### Others

|   Module   | Version |  Description     |
|------------|---------|------------------|
| FSM        | 1.1.0   | State Machine    |
| StarGate   | 1.1.0   | Transport        |
| LNC        | 0.2.1   | Notification     |
| DOS        | 0.1.3   | File System      |


## Architecture Diagram

<style>
pre code {
    font-family: "Lucida Console", "Consolas", Monaco, monospace;
    line-height: 0px;
}
</style>

```
          
          
                 +-------+        +--------+        +-------+
          .....> |  SDK  | .....> |  DIMP  | .....> |  DKD  |
          :      +-------+        +--------+        +-------+
          :                           ^                 :
          :                           :                 V
          :          +-----------+    :             +-------+      +--------+
          :........> |  Plugins  | ...:             |  MKM  | ...> | Crypto |
          :          +-----------+                  +-------+      +--------+
          :
    +==========+
    |  SEChat  |
    +==========+
          :
          :     +-------+
          :...> |  LNC  |
          :     +-------+
          :     
          :     +-------+
          :...> |  DOS  |
          :     +-------+
          :
          :     +------------+       +-------+     +----------+     +-------+
          :...> |  StarGate  | ....> |  TCP  | ..> | StarTrek | ..> |  FSM  |
          :     +------------+       +-------+     +----------+     +-------+
          :            :                                ^
          :            :             +-------+          :
          :            :...........> |  UDP  | .........:
          :                          +-------+          :
          :                                             V
          :     +--------+                          +-------+           
          :...> |  DMTP  | .......................> |  MTP  | ...........
                +--------+            :             +-------+           :
                                      V                                 V
                +--------+        +--------+        +-------+        +------+
                |  TURN  | .....> |  STUN  | .....> |  TLV  | .....> |  BA  |
                +--------+        +--------+        +-------+        +------+


```

--
<i>Edited by [Alber Moky](https://twitter.com/AlbertMoky) @ 2023-3-25</i>