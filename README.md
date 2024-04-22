
# rag-ocp-sample


1) RAG_with_sources_Langchain-Caikit.ipynb - tested with Chroma vector DB + Ollama server at http://ollama.myredis.svc.cluster.local:11434

2) gradio-caikit-rag-redis - Ollama INFERENCE_SERVER_URL http://ollama.myredis.svc.cluster.local:11434 and REDIS_URL : redis://default:Jj2BldyH@my-doc-headless.myredis.svc.cluster.local:18586


apiVersion: app.redislabs.com/v1
kind: RedisEnterpriseCluster
metadata:
  name: rec
spec:
  serviceAccountName: rec
  redisEnterpriseNodeResources:
    limits:
      cpu: '4'
      ephemeral-storage: 10Gi
      memory: 6Gi
    requests:
      cpu: '4'
      ephemeral-storage: 1Gi
      memory: 6Gi
  bootstrapperImageSpec:
    repository: registry.connect.redhat.com/redislabs/redis-enterprise-operator
  clusterCredentialSecretName: rec
  nodes: 1
  persistentSpec:
    enabled: true
    storageClassName: gp3-csi
    volumeSize: 20Gi
  createServiceAccount: true
  username: admin@redhat.com
  clusterCredentialSecretRole: ''
  podStartingPolicy:
    enabled: false
    startingThresholdSeconds: 540
  redisEnterpriseServicesRiggerImageSpec:
    repository: registry.connect.redhat.com/redislabs/services-manager
  redisEnterpriseImageSpec:
    imagePullPolicy: IfNotPresent
    repository: registry.connect.redhat.com/redislabs/redis-enterprise
  uiServiceType: ClusterIP
  clusterCredentialSecretType: kubernetes
  servicesRiggerSpec:
    databaseServiceType: 'cluster_ip,headless'
    serviceNaming: bdb_name
  services:
    apiService:
      type: ClusterIP
      
      
      
apiVersion: app.redislabs.com/v1alpha1
kind: RedisEnterpriseDatabase
metadata:
  name: my-doc
spec:
  memorySize: 4GB
  modulesList:
    - name: search
      version: 2.8.11
  persistence: snapshotEvery12Hour
  replication: false
  tlsMode: disabled
  type: redis
  
  

oc adm policy add-scc-to-user redis-enterprise-scc system:serviceaccount:myredis:redis-enterprise-operator
oc adm policy add-scc-to-user redis-enterprise-scc system:serviceaccount:myredis:rec

redis://default:Jj2BldyH@my-doc-headless.myredis.svc.cluster.local:18586

redis://admin@redhat.com:zn26W36e@my-doc-headless.redis.svc.cluster.local:15379


- Add pdf folder with a sample pdf


pip install caikit-nlp-client
pip install langchain



https://redis.io/docs/latest/operate/kubernetes/delete-custom-resources/
oc patch rec rec --type=json -p \
    '[{"op":"remove","path":"/metadata/finalizers","value":"redbfinalizer.redisenterpriseclusters.app.redislabs.com"}]'      
      

https://github.com/opendatahub-io-contrib/workbench-images - Jupyter Langchain (CUDA) 


llm-on-openshift/examples/notebooks/langchain/Langchain-Redis-Query.ipynb - step3 - schema=schema_name incorrect      


redis-cli -h localhost -p 18586 -a Jj2BldyH
FT._LIST


