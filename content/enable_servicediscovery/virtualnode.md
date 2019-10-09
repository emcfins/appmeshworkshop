---
title: "Create a new virtual node"
date: 2018-09-18T17:39:30-05:00
weight: 20
---

* Create a second virtual node for the crystal backend, and use service discovery instead.

```bash
SPEC=$(cat <<-EOF
    { 
      "serviceDiscovery": {
        "awsCloudMap": {
          "namespaceName": "appmeshworkshop.pvt.local",
          "serviceName": "crystal"
        }
      },
      "logging": {
        "accessLog": {
          "file": {
            "path": "/dev/stdout"
          }
        }
      },      
      "listeners": [
        {
          "portMapping": { "port": 3000, "protocol": "http" }
        }
      ]
    }
EOF
); \
aws appmesh create-virtual-node \
      --mesh-name appmesh-workshop \
      --virtual-node-name crystal-srv-v1 \
      --spec "$SPEC"
```