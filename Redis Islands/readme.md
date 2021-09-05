1.
ssh node01
mkdir redis01
mkdir redis02
mkdir redis03
mkdir redis04
mkdir redis05
mkdir redis06

2.
kap pv.yaml
kap redis-cluster-statefulset.yaml

3. 
kubectl exec -it redis-cluster-0 -- redis-cli --cluster create --cluster-replicas 1 $(kubectl get pods -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')

4. 
kap service.yaml