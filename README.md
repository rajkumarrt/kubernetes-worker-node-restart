# kubernetes-worker-node-restart
Kubernetes worker node restart

<p><strong><u>Restart of node (Perform this activity in Master node)</u></strong></p>
<p>root@k8-pr-master:~# <span style="color: #ff6600;">kubectl get nodes</span></p>
<p>NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; STATUS&nbsp;&nbsp; ROLES&nbsp;&nbsp;&nbsp; AGE&nbsp;&nbsp; VERSION</p>
<p>k8-pr-master&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; master&nbsp;&nbsp; 20h&nbsp;&nbsp; v1.18.1</p>
<p>k8-pr-woker1&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 19h&nbsp;&nbsp; v1.18.1</p>
<p>kb-pr-worker2&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 36m&nbsp;&nbsp; v1.18.1</p>
<p>&nbsp;</p>
<p><strong>#Drain the node in worker2 node2</strong></p>
<p>root@k8-pr-master:~#&nbsp; <span style="color: #ff6600;">kubectl drain --ignore-daemonsets --force --delete-local-data kb-pr-worker2</span></p>
<p>Flag --delete-local-data has been deprecated, This option is deprecated and will be deleted. Use --delete-emptydir-data.</p>
<p>node/kb-pr-worker2 cordoned</p>
<p>WARNING: ignoring DaemonSet-managed Pods: kube-system/calico-node-4hrtp, kube-system/kube-proxy-kdfhc</p>
<p>evicting pod default/nginx-deployment-d46f5678b-js8tl</p>
<p>evicting pod default/nginx-deployment-d46f5678b-hntfv</p>
<p>pod/nginx-deployment-d46f5678b-hntfv evicted</p>
<p>pod/nginx-deployment-d46f5678b-js8tl evicted</p>
<p>node/kb-pr-worker2 evicted</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>Note: To force termination of any problematic pods, use the following command:</strong></p>
<p>&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;<span style="color: #ff6600;">kubectl delete pod &lt;pod_name&gt; -n=&lt;pod_namespace&gt; --grace-period=0 --force</span></p>
<p>&nbsp;</p>
<p>#Check the cordon status</p>
<p>root@k8-pr-master:~#<span style="color: #ff6600;"> kubectl cordon kb-pr-worker2</span></p>
<p>node/kb-pr-worker2 already cordoned</p>
<p>&nbsp;</p>
<p>root@k8-pr-master:~#<span style="color: #ff6600;"> kubectl get nodes</span></p>
<p>NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; STATUS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ROLES&nbsp;&nbsp;&nbsp; AGE&nbsp;&nbsp; VERSION</p>
<p>k8-pr-master&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; master&nbsp;&nbsp; 20h&nbsp;&nbsp; v1.18.1</p>
<p>k8-pr-woker1&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 19h&nbsp;&nbsp; v1.18.1</p>
<p>kb-pr-worker2&nbsp;&nbsp; Ready,SchedulingDisabled&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 37m&nbsp;&nbsp; v1.18.1</p>
<p>&nbsp;</p>
<p><strong>#All pods are moved to worker1 node</strong></p>
<p>root@k8-pr-master:~# <span style="color: #ff6600;">kubectl get pods -o wide</span></p>
<p>NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; READY&nbsp;&nbsp; STATUS&nbsp;&nbsp;&nbsp; RESTARTS&nbsp;&nbsp; AGE&nbsp;&nbsp; IP&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NODE&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NOMINATED NODE&nbsp;&nbsp; READINESS GATES</p>
<p>nginx-deployment-d46f5678b-k4xp8&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 31s&nbsp;&nbsp; 10.10.240.198&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-kt8qg&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 31s&nbsp;&nbsp; 10.10.240.197&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-l5p8n&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 19h&nbsp;&nbsp; 10.10.240.195&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-q65pj&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 19h&nbsp;&nbsp; 10.10.240.196&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>&nbsp;</p>
<p><strong>#View the pod details in particular node</strong></p>
<p>root@k8-pr-master:~#&nbsp;&nbsp;<span style="color: #ff6600;"> kubectl get pods -o wide --all-namespaces --field-selector=spec.nodeName==kb-pr-worker2</span></p>
<p>NAMESPACE&nbsp;&nbsp;&nbsp;&nbsp; NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; READY&nbsp;&nbsp; STATUS&nbsp;&nbsp;&nbsp; RESTARTS&nbsp;&nbsp; AGE&nbsp;&nbsp; IP&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NODE&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NOMINATED NODE&nbsp;&nbsp; READINESS GATES</p>
<p>kube-system&nbsp;&nbsp; calico-node-4hrtp&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 38m&nbsp;&nbsp; 192.168.10.8&nbsp;&nbsp; kb-pr-worker2&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>kube-system&nbsp;&nbsp; kube-proxy-kdfhc&nbsp;&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 38m&nbsp;&nbsp; 192.168.10.8&nbsp;&nbsp; kb-pr-worker2&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>&nbsp;</p>
<p><strong>#After reboot of the worker2 node, uncordon</strong></p>
<p>root@k8-pr-master:~# <span style="color: #ff6600;">kubectl uncordon kb-pr-worker2</span></p>
<p>node/kb-pr-worker2 uncondoned</p>
<p>&nbsp;</p>
<p>root@k8-pr-master:~# <span style="color: #ff6600;">kubectl get nodes</span></p>
<p>NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; STATUS&nbsp;&nbsp; ROLES&nbsp;&nbsp;&nbsp; AGE&nbsp;&nbsp; VERSION</p>
<p>k8-pr-master&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; master&nbsp;&nbsp; 20h&nbsp;&nbsp; v1.18.1</p>
<p>k8-pr-woker1&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 19h&nbsp;&nbsp; v1.18.1</p>
<p>kb-pr-worker2&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 38m&nbsp;&nbsp; v1.18.1</p>
<p>&nbsp;</p>
<p>root@k8-pr-master:~# <span style="color: #ff6600;">kubectl get pods -o wide</span></p>
<p>NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; READY&nbsp;&nbsp; STATUS&nbsp;&nbsp;&nbsp; RESTARTS&nbsp;&nbsp; AGE&nbsp;&nbsp;&nbsp; IP&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NODE&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NOMINATED NODE&nbsp;&nbsp; READINESS GATES</p>
<p>nginx-deployment-d46f5678b-k4xp8&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2m4s&nbsp;&nbsp; 10.10.240.198&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-kt8qg&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2m4s&nbsp;&nbsp; 10.10.240.197&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-l5p8n&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 19h&nbsp;&nbsp;&nbsp; 10.10.240.195&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-q65pj&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 19h&nbsp;&nbsp;&nbsp; 10.10.240.196&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>&nbsp;</p>
<p><strong>#Incase load is less, pods will not move to worker node 2. Just create addl node (replica) --- Testing</strong></p>
<p>root@k8-pr-master:~# <span style="color: #ff6600;">kubectl apply -f sampledeploy.yaml</span></p>
<p>deployment.apps/nginx-deployment configured</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>root@k8-pr-master:~#<span style="color: #ff6600;"> kubectl get pods -o wide</span></p>
<p>NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; READY&nbsp;&nbsp; STATUS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; RESTARTS&nbsp;&nbsp; AGE&nbsp;&nbsp;&nbsp;&nbsp; IP&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NODE&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NOMINATED NODE&nbsp;&nbsp; READINESS GATES</p>
<p>nginx-deployment-d46f5678b-8jw8r&nbsp;&nbsp; 0/1&nbsp;&nbsp;&nbsp;&nbsp; ContainerCreating&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 5s&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; kb-pr-worker2&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-jfrps&nbsp;&nbsp; 0/1&nbsp;&nbsp;&nbsp;&nbsp; ContainerCreating&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 5s&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; kb-pr-worker2&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-k4xp8&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 4m31s&nbsp;&nbsp; 10.10.240.198&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-kt8qg&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 4m31s&nbsp;&nbsp; 10.10.240.197&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-l5p8n&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 19h&nbsp;&nbsp;&nbsp;&nbsp; 10.10.240.195&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>nginx-deployment-d46f5678b-q65pj&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 19h&nbsp;&nbsp;&nbsp;&nbsp; 10.10.240.196&nbsp;&nbsp; k8-pr-woker1&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>&nbsp;</p>
<p>root@k8-pr-master:~#&nbsp;&nbsp; <span style="color: #ff6600;">Kubectl get pods -o wide --all-namespaces --field-selector=spec.nodeName==kb-pr-worker2</span></p>
<p>NAMESPACE&nbsp;&nbsp;&nbsp;&nbsp; NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;READY&nbsp;&nbsp; STATUS&nbsp;&nbsp;&nbsp; RESTARTS&nbsp;&nbsp; AGE&nbsp;&nbsp;&nbsp; IP&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NODE&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NOMINATED NODE&nbsp;&nbsp; READINESS GATES</p>
<p>default&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nginx-deployment-d46f5678b-8jw8r&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2m9s&nbsp;&nbsp; 10.10.82.196&nbsp;&nbsp; kb-pr-worker2&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>default&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;nginx-deployment-d46f5678b-jfrps&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2m9s&nbsp;&nbsp; 10.10.82.195&nbsp;&nbsp; kb-pr-worker2&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;</p>
<p>kube-system&nbsp;&nbsp; calico-node-4hrtp&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 43m&nbsp;&nbsp;&nbsp; 192.168.10.8&nbsp;&nbsp; kb-pr-worker2&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&lt;none&gt;</p>
<p>kube-system&nbsp;&nbsp; kube-proxy-kdfhc&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 43m&nbsp;&nbsp;&nbsp; 192.168.10.8&nbsp;&nbsp; kb-pr-worker2&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</p>
