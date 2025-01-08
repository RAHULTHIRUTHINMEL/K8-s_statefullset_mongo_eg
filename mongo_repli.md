rs.initiate(
   {
      _id: "rs0",
      members: [
         { _id: 0, host : "mongo-0.mongo.default.svc.cluster.local:27017" },
         { _id: 1, host : "mongo-1.mongo.default.svc.cluster.local:27017" },
         { _id: 2, host : "mongo-2.mongo.default.svc.cluster.local:27017" }
      ]
   }
)

here in statefulsets beforehand  we have to apply pvc and storage claims, and the SC provisions pv dynamically cause we mention it in sc.yaml how it is provisioned. The ServiceName in statefulsets points to headless service we create, later  that the StatefulSet uses to manage the network identities of its pods. 

command given above is the intiation of the replica set, rs0 is the replicaset name in statefulset.yaml . after the excution of the above command, the node chnages to primary, ie mongo0-primary and other nodes become secondary nodes.we have to do it manually. 


The serviceName ensures that pods in the StatefulSet can discover and communicate with each other using predictable hostnames. This is critical for:

Replica sets (MongoDB): Each pod in the set knows how to connect to others and serviceName in SS.yaml Ensures stable DNS hostnames for pods.


to set up to enable read in secondary use command rs.slaveok().  after this data is replicated on slave and slave 2 and is odne by headless service.
