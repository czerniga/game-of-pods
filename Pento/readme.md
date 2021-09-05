1.
get log from api server container
    docker ps -a | grep api
    docker logs k8s_kube-apiserver_kube-apiserver-controlplane_kube-system_XXXXXX

2. 
check error (unable to load client CA file: unable to load client CA file: open /etc/kubernetes/pki/ca-authority.crt: no such file or directory)

3. 
change path to crt file:
    vi /etc/kubernetes/manifests/kube-apiserver.yaml
     - --client-ca-file=/etc/kubernetes/pki/ca-authority.crt -->  - --etcd-cafile=/etc/kubernetes/pki/etcd/ca.crt

4. 
wait for container restart

5.
change port in kube config
    vi ~/.kube/config
    server: https://172.17.0.11:2379 --> https://172.17.0.11:6443

6.
change image for coredns delpoyment
    kubectl edit deployments --namespace=kube-system coredns 
    image: k8s.gcr.io/kubedns:1.3.1 --> image: k8s.gcr.io/coredns:1.3.1

7. 
fix worker node
    kubectl uncordon node01