
# rag-ocp-sample


oc new-project redis

oc apply -f scc.yaml



oc adm policy add-scc-to-user redis-enterprise-scc system:serviceaccount:redis:redis-enterprise-operator
oc adm policy add-scc-to-user redis-enterprise-scc system:serviceaccount:redis:rec
 
 

https://github.com/rh-aiservices-bu/llm-on-openshift/tree/main/vector-databases/redis

oc apply -f rec.yaml
oc apply -f rec-db.yaml

redis://default:O4jGUYsT@my-doc-headless.redis.svc.cluster.local:14845


You can either install Langchain and its dependencies in your workbench (pip install langchain), or you can directly use a pre-built custom Workbench image that comes with everything needed: 
quay.io/opendatahub-contrib/workbench-images:cuda-jupyter-langchain-c9s-py311_2023c_latest.

Create workbench with above image

rag-ocp-sample/Langchain-Redis-Ingest.ipynb   - Update redis URL and Ingest Data




  