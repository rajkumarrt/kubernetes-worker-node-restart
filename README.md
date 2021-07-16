<p><span style="font-size:11pt"><span style="font-family:Calibri,sans-serif"><strong><u>Restart of node (Perform this activity in Master node)</u></strong></span></span></p>

<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="kubectl get nodes"><pre><code>
root@k8-pr-master:~# kubectl get nodes
NAME            STATUS   ROLES    AGE   VERSION
k8-pr-master    Ready    master   20h   v1.18.1
k8-pr-woker1    Ready    <none>   19h   v1.18.1
kb-pr-worker2   Ready    <none>   36m   v1.18.1
</code></pre></div>

<h3> #Drain the node in worker2 node2 </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="kubectl get nodes"><pre><code>
root@k8-pr-master:~#  kubectl drain --ignore-daemonsets --force --delete-local-data kb-pr-worker2
Flag --delete-local-data has been deprecated, This option is deprecated and will be deleted. Use --delete-emptydir-data.
node/kb-pr-worker2 cordoned
WARNING: ignoring DaemonSet-managed Pods: kube-system/calico-node-4hrtp, kube-system/kube-proxy-kdfhc
evicting pod default/nginx-deployment-d46f5678b-js8tl
evicting pod default/nginx-deployment-d46f5678b-hntfv
pod/nginx-deployment-d46f5678b-hntfv evicted
pod/nginx-deployment-d46f5678b-js8tl evicted
node/kb-pr-worker2 evicted
</code></pre></div>

<h3> #To force termination of any problematic pods, use the following command</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="kubectl get nodes"><pre><code>
kubectl delete pod <pod_name> -n=<pod_namespace> --grace-period=0 --force
</code></pre></div>

<h3> #After cordon pod detail is</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="kubectl get nodes"><pre><code>
root@k8-pr-master:~# kubectl get nodes
NAME            STATUS                     ROLES    AGE   VERSION
k8-pr-master    Ready                      master   20h   v1.18.1
k8-pr-woker1    Ready                      <none>   19h   v1.18.1
kb-pr-worker2   Ready,SchedulingDisabled   <none>   37m   v1.18.1
</code></pre></div>

<h3> #All the pods were moved worker node1</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="kubectl get nodes"><pre><code>
root@k8-pr-master:~# kubectl get pods -o wide
NAME                               READY   STATUS    RESTARTS   AGE   IP              NODE           NOMINATED NODE   READINESS GATES
nginx-deployment-d46f5678b-k4xp8   1/1     Running   0          31s   10.10.240.198   k8-pr-woker1   <none>           <none>
nginx-deployment-d46f5678b-kt8qg   1/1     Running   0          31s   10.10.240.197   k8-pr-woker1   <none>           <none>
nginx-deployment-d46f5678b-l5p8n   1/1     Running   1          19h   10.10.240.195   k8-pr-woker1   <none>           <none>
nginx-deployment-d46f5678b-q65pj   1/1     Running   1          19h   10.10.240.196   k8-pr-woker1   <none>           <none>
</code></pre></div>

<h3> #View the pod details in particular node</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="kubectl get nodes"><pre><code>
root@k8-pr-master:~#   kubectl get pods -o wide --all-namespaces --field-selector=spec.nodeName==kb-pr-worker2
NAMESPACE     NAME                READY   STATUS    RESTARTS   AGE   IP             NODE            NOMINATED NODE   READINESS GATES
kube-system   calico-node-4hrtp   1/1     Running   0          38m   192.168.10.8   kb-pr-worker2   <none>           <none>
kube-system   kube-proxy-kdfhc    1/1     Running   0          38m   192.168.10.8   kb-pr-worker2   <none>           <none>
</code></pre></div>

<h3> #After reboot of the worker2 node, uncordon</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="kubectl get nodes"><pre><code>
root@k8-pr-master:~# kubectl uncordon kb-pr-worker2
node/kb-pr-worker2 uncondoned

#Pod is ready
root@k8-pr-master:~# kubectl get nodes
NAME            STATUS   ROLES    AGE   VERSION
k8-pr-master    Ready    master   20h   v1.18.1
k8-pr-woker1    Ready    <none>   19h   v1.18.1
kb-pr-worker2   Ready    <none>   38m   v1.18.1

root@k8-pr-master:~# kubectl get pods -o wide
NAME                               READY   STATUS              RESTARTS   AGE     IP              NODE            NOMINATED NODE   READINESS GATES
nginx-deployment-d46f5678b-8jw8r   0/1     ContainerCreating   0          5s      <none>          kb-pr-worker2   <none>           <none>
nginx-deployment-d46f5678b-jfrps   0/1     ContainerCreating   0          5s      <none>          kb-pr-worker2   <none>           <none>
nginx-deployment-d46f5678b-k4xp8   1/1     Running             0          4m31s   10.10.240.198   k8-pr-woker1    <none>           <none>
nginx-deployment-d46f5678b-kt8qg   1/1     Running             0          4m31s   10.10.240.197   k8-pr-woker1    <none>           <none>
nginx-deployment-d46f5678b-l5p8n   1/1     Running             1          19h     10.10.240.195   k8-pr-woker1    <none>           <none>
nginx-deployment-d46f5678b-q65pj   1/1     Running             1          19h     10.10.240.196   k8-pr-woker1    <none>           <none>

</code></pre></div>



![visitors](https://visitor-badge.glitch.me/badge?page_id=rajkumarrt.visitor-badge)
