<p><span style="font-size:11pt"><span style="font-family:Calibri,sans-serif"><strong><u>Restart of node (Perform this activity in Master node)</u></strong></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">root@k8-pr-master:~# <span style="background-color:yellow">kubectl get nodes</span></span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; STATUS&nbsp;&nbsp; ROLES&nbsp;&nbsp;&nbsp; AGE&nbsp;&nbsp; VERSION</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">k8-pr-master&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; master&nbsp;&nbsp; 20h&nbsp;&nbsp; v1.18.1</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">k8-pr-woker1&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 19h&nbsp;&nbsp; v1.18.1</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">kb-pr-worker2&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 36m&nbsp;&nbsp; v1.18.1</span></span></span></span></span></span></span></p>

<p>&nbsp;</p>

<p><strong><span style="font-size:11pt"><span style="font-family:Calibri,sans-serif">#Drain the node in worker2 node2</span></span></strong></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">root@k8-pr-master:~#&nbsp; <span style="background-color:yellow">kubectl drain --ignore-daemonsets --force --delete-local-data kb-pr-worker2</span></span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">Flag --delete-local-data has been deprecated, This option is deprecated and will be deleted. Use --delete-emptydir-data.</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">node/kb-pr-worker2 cordoned</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">WARNING: ignoring DaemonSet-managed Pods: kube-system/calico-node-4hrtp, kube-system/kube-proxy-kdfhc</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">evicting pod default/nginx-deployment-d46f5678b-js8tl</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">evicting pod default/nginx-deployment-d46f5678b-hntfv</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">pod/nginx-deployment-d46f5678b-hntfv evicted</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">pod/nginx-deployment-d46f5678b-js8tl evicted</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">node/kb-pr-worker2 evicted</span></span></span></span></span></span></span></p>

<p>&nbsp;</p>

<p>&nbsp;</p>

<p><strong><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">Note: To force termination of any problematic pods, use the following command:</span></span></span></span></span></span></span></strong></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;<span style="background-color:yellow">kubectl delete pod &lt;pod_name&gt; -n=&lt;pod_namespace&gt; --grace-period=0 --force</span></span></span></span></span></span></span></span></p>

<p>&nbsp;</p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">root@k8-pr-master:~# <span style="background-color:yellow">kubectl cordon kb-pr-worker2</span></span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">node/kb-pr-worker2 already cordoned</span></span></span></span></span></span></span></p>

<p>&nbsp;</p>

<p>&nbsp;</p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">root@k8-pr-master:~# <span style="background-color:yellow">kubectl get nodes</span></span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; STATUS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ROLES&nbsp;&nbsp;&nbsp; AGE&nbsp;&nbsp; VERSION</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">k8-pr-master&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; master&nbsp;&nbsp; 20h&nbsp;&nbsp; v1.18.1</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">k8-pr-woker1&nbsp;&nbsp;&nbsp; Ready&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 19h&nbsp;&nbsp; v1.18.1</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">kb-pr-worker2&nbsp;&nbsp; Ready,SchedulingDisabled&nbsp;&nbsp; &lt;none&gt;&nbsp;&nbsp; 37m&nbsp;&nbsp; v1.18.1</span></span></span></span></span></span></span></p>

<p>&nbsp;</p>

<p><strong><span style="font-size:11pt"><span style="font-family:Calibri,sans-serif">#All pods are moved to worker1 node</span></span></strong></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">root@k8-pr-master:~# <span style="background-color:yellow">kubectl get pods -o wide</span></span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; READY&nbsp;&nbsp; STATUS&nbsp;&nbsp;&nbsp; RESTARTS&nbsp;&nbsp; AGE&nbsp;&nbsp; IP&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NODE&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; NOMINATED NODE&nbsp;&nbsp; READINESS GATES</span></span></span></span></span></span></span></p>

<p><span style="background-color:whitesmoke"><span style="font-size:11pt"><span style="background-color:whitesmoke"><span style="font-family:Calibri,sans-serif"><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">nginx-deployment-d46f5678b-k4xp8&nbsp;&nbsp; 1/1&nbsp;&nbsp;&nbsp;&nbsp; Running&nbsp;&nbsp; 0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 31s&nbsp;&nbsp; 10.10.240.198&nbsp;&nbsp; </span></span></span><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:red">k8-pr-woker1&nbsp;&nbsp; </span></span></span><span style="font-size:10.0pt"><span style="font-family:Consolas"><span style="color:#333333">&lt;none&gt;&nbsp;&nbsp;&nbsp;&nbsp

 ![visitors](https://visitor-badge.glitch.me/badge?page_id=rajkumarrt.visitor-badge)
