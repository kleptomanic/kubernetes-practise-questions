# 400 Basic Kubernetes Practical Questions for CKA, CKAD, and CKS

These questions are designed to prepare you for the Certified Kubernetes Administrator (CKA), Certified Kubernetes Application Developer (CKAD), and Certified Kubernetes Security Specialist (CKS) exams. They focus on practical, hands-on tasks that mimic real-world production scenarios, covering essential Kubernetes resources such as pods, deployments, services, networking, storage, security, and resource management. Each task reflects common activities in production environments, such as deploying scalable microservices, securing sensitive workloads, and optimizing resource usage.

## Cluster Setup and Management (1-50)

1. Install `minikube` on a Linux machine and start a single-node cluster with containerd as the runtime.
2. Verify the cluster is running using `kubectl cluster-info` and check the Kubernetes version with `kubectl version`.
3. List all nodes in the cluster using `kubectl get nodes` and verify their status.
4. Label a node with `env=production` using `kubectl label node <node-name> env=production`.
5. Cordon a worker node to prevent scheduling using `kubectl cordon <node-name>`.
6. Drain a node for maintenance using `kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data`.
7. Uncordon the node to allow scheduling using `kubectl uncordon <node-name>`.
8. Create a namespace named `ecommerce` for an online store application using `kubectl create namespace ecommerce`.
9. Set the current context to the `ecommerce` namespace using `kubectl config set-context --current --namespace=ecommerce`.
10. List all namespaces in the cluster using `kubectl get namespaces`.
11. Delete a namespace named `test` using `kubectl delete namespace test`.
12. Check the status of control plane components using `kubectl get componentstatuses`.
13. View the current kubeconfig settings using `kubectl config view`.
14. Switch to a different context using `kubectl config use-context <context-name>`.
15. Create a new user `app-admin` and generate a kubeconfig file for cluster access.
16. Backup the etcd database using `etcdctl snapshot save /backup/etcd-snapshot.db`.
17. Restore the etcd database from a snapshot using `etcdctl snapshot restore /backup/etcd-snapshot.db`.
18. Initialize a multi-node cluster using `kubeadm init` and join a worker node with `kubeadm join`.
19. Remove a worker node from the cluster using `kubectl delete node <node-name>`.
20. Install the Calico CNI plugin in the cluster and verify pod networking.
21. Deploy the Kubernetes dashboard and access it using `kubectl proxy`.
22. Configure cluster autoscaling for worker nodes in a cloud provider like AWS.
23. Set up a high-availability control plane with stacked masters using `kubeadm`.
24. Enable audit logging for the Kubernetes API server and verify logs in `/var/log/kube-apiserver`.
25. Configure the API server to use OIDC authentication with a provider like Keycloak.
26. Label all nodes with `region=us-west` for regional workload placement.
27. Create a namespace named `payment` for a payment processing service.
28. Configure a custom scheduler named `app-scheduler` for specific workloads.
29. Set up the cluster to pull images from a private registry like `docker.io/private`.
30. Enable pod priority and preemption using a `PriorityClass` named `high-priority`.
31. Create a ResourceQuota for CPU (4 cores) and memory (8Gi) in the `ecommerce` namespace.
32. Set up a default StorageClass for dynamic provisioning with AWS EBS.
33. Install `metrics-server` to enable resource usage monitoring with `kubectl top`.
34. Deploy Fluentd to collect and forward cluster logs to an external logging service.
35. Install Prometheus to monitor cluster metrics and verify node metrics collection.
36. Configure Alertmanager to send alerts for high CPU usage in the cluster.
37. Install `cert-manager` to manage TLS certificates for Ingress resources.
38. Deploy `external-dns` to sync service DNS records with Route 53.
39. Set up Velero to back up and restore the `ecommerce` namespace.
40. Install Kyverno to enforce pod security policies in the cluster.
41. Deploy ArgoCD for GitOps-based application deployments.
42. Upgrade a cluster to a specific Kubernetes version using `kubeadm upgrade`.
43. Join a new worker node to the cluster using a token generated by `kubeadm token create`.
44. Configure the cluster to use CRI-O as the container runtime.
45. Enable RBAC authorization in the cluster and verify with `kubectl auth can-i`.
46. Apply a taint `key=dedicated,value=app,effect=NoSchedule` to a node.
47. Create a namespace named `inventory` for an inventory management system.
48. Configure CoreDNS with a custom upstream DNS server for external resolution.
49. Set up a LimitRange in the `payment` namespace to enforce pod resource limits.
50. Verify cluster health using `kubectl get --raw=/healthz`.

## Pods and Containers (51-120)

51. Create a pod named `frontend-pod` with the `nginx:1.21` image in the `ecommerce` namespace using `kubectl run`.
52. Create a pod with two containers (`nginx` and `redis`) for a web application in the `payment` namespace.
53. Set environment variables `APP_ENV=prod` and `LOG_LEVEL=info` in a pod using a ConfigMap.
54. Configure a liveness probe for a pod checking HTTP GET on `/health` at port 80.
55. Create a pod with an init container to create a file `/data/config.txt` before the main container starts.
56. Create a pod that runs `echo "Order processed"` and exits using `busybox`.
57. View logs of the `frontend-pod` pod using `kubectl logs frontend-pod`.
58. Exec into the `frontend-pod` pod and run `nginx -v` using `kubectl exec`.
59. Describe the `frontend-pod` pod to check its configuration using `kubectl describe pod`.
60. Delete the `frontend-pod` pod using `kubectl delete pod frontend-pod`.
61. Create a pod with label `app=frontend` in the `inventory` namespace.
62. List all pods with label `app=frontend` using `kubectl get pods -l app=frontend`.
63. Create a pod with CPU request of 0.5 and memory limit of 512Mi in the `ecommerce` namespace.
64. Configure a readiness probe for a pod checking TCP port 8080.
65. Create a pod using a service account named `web-sa` in the `payment` namespace.
66. Mount a ConfigMap named `web-config` as a volume in a pod at `/etc/config`.
67. Mount a Secret named `db-secret` as a volume in a pod at `/etc/secrets`.
68. Create a pod with a `hostPath` volume mounted at `/var/data` for logging.
69. Configure a pod to run on a node labeled `env=production`.
70. Set up a pod with affinity to co-locate with pods labeled `app=backend`.
71. Create a pod with anti-affinity to avoid scheduling on nodes with `app=backend`.
72. Configure a pod to tolerate a taint `key=dedicated,value=app,effect=NoSchedule`.
73. Set a DNS policy of `ClusterFirst` for a pod running a microservice.
74. Create a pod with a restart policy of `Never` for a one-time task.
75. Configure a pod with an image pull policy of `IfNotPresent` for a stable image.
76. Set a termination grace period of 60 seconds for a pod handling HTTP requests.
77. Create a pod exposing ports 80 (HTTP) and 443 (HTTPS).
78. Configure a pod with a security context setting `runAsUser: 1000` for a web app.
79. Set up a pod to run as a non-root user with `runAsNonRoot: true`.
80. Create a pod with dropped capability `NET_RAW` for security.
81. Configure a pod with a custom sysctl `net.core.somaxconn=1024` for high traffic.
82. Set up a pod with a read-only root filesystem for a stateless application.
83. Create a pod using the Weave Net CNI plugin for networking.
84. Configure a pod to use a StorageClass named `fast` for persistent storage.
85. Set up a pod with a projected volume combining a ConfigMap and Secret.
86. Create a pod using the downward API to expose pod name and namespace.
87. Mount a ConfigMap with `subPath: config.yaml` in a pod at `/app/config`.
88. Configure a pod with a `hostAliases` entry for `api.internal` resolving to `10.0.0.1`.
89. Create a pod using Docker as the container runtime for a legacy app.
90. Configure a pod to run a custom command `python app.py` for a Python app.
91. Set up a pod to execute a shell script from a ConfigMap.
92. Create a pod that sleeps for 2 hours using `sleep 7200` for a long-running task.
93. Configure a pod to run `/bin/echo "Payment processed"` for a transaction log.
94. Set environment variables in a pod from a Secret named `api-secret`.
95. Create a pod with environment variables from a ConfigMap for app settings.
96. Configure a pod to use a specific image tag `redis:6.2` for a cache service.
97. Set up a pod with a sidecar container logging to `/var/log/app.log`.
98. Create a pod with an ambassador container proxying traffic to port 8080.
99. Configure a pod with an adapter container modifying API responses.
100. Set up a pod with two init containers for database and cache initialization.
101. Create a pod with an `emptyDir` volume for temporary session data.
102. Mount a PersistentVolumeClaim named `data-pvc` in a pod for a database.
103. Configure a pod to mount a host directory `/var/log/app` for logging.
104. Create a pod with a volume from a ConfigMap named `app-settings`.
105. Mount a Secret named `tls-secret` as a volume in a pod for HTTPS.
106. Set up a projected volume combining `app-settings` and `tls-secret` in a pod.
107. Create a pod exposing pod labels via the downward API for monitoring.
108. Configure a pod to expose container port 8080 for a web server.
109. Set up a pod with a host port mapping to 8080 for external access.
110. Create a pod using UDP protocol for port 53 for a DNS resolver.
111. Configure a pod with a memory request of 256Mi for a lightweight service.
112. Create a pod with a CPU limit of 0.2 for a low-priority task.
113. Set up a pod with a `hostPath` volume type `DirectoryOrCreate` for logs.
114. Configure a pod to tolerate a taint `key=app,value=prod,effect=PreferNoSchedule`.
115. Create a pod with a specific image pull secret for a private registry.
116. Set up a pod with a custom termination message path `/tmp/termination.log`.
117. Configure a pod with a liveness probe timeout of 5 seconds.
118. Create a pod with a readiness probe initial delay of 10 seconds.
119. Set up a pod with a volume mount for a ConfigMap with `defaultMode: 0400`.
120. Configure a pod to use a specific pod security context for group ID 2000.

## Workload Management (121-190)

121. Create a deployment named `store-front` with 3 replicas using `nginx:1.21` in the `ecommerce` namespace.
122. Scale the `store-front` deployment to 5 replicas using `kubectl scale deployment store-front --replicas=5`.
123. Update the `store-front` deployment to use `nginx:1.22` using `kubectl set image`.
124. Roll back the `store-front` deployment to the previous version using `kubectl rollout undo`.
125. Create a StatefulSet named `cassandra-db` with 3 replicas in the `inventory` namespace.
126. Create a Job named `data-import` with 5 completions using `busybox` to process data files.
127. Create a CronJob named `daily-report` that runs every day at 1 AM using `busybox`.
128. Configure a HorizontalPodAutoscaler for `store-front` to scale based on 80% CPU usage.
129. Set up a VerticalPodAutoscaler for `store-front` to auto-adjust CPU and memory resources.
130. Create a ReplicaSet named `api-rs` with 4 replicas using `httpd:2.4` in the `payment` namespace.
131. Update the `api-rs` ReplicaSet to use `httpd:2.4.48` and verify the change.
132. Delete the `api-rs` ReplicaSet and confirm pod termination using `kubectl delete rs`.
133. Create a deployment with a label selector `app=store` for a retail application.
134. Configure a rolling update strategy for `store-front` with `maxSurge=1` and `maxUnavailable=0`.
135. Set up a canary deployment for `store-front` using a second deployment with `nginx:1.23`.
136. Configure a readiness gate for `store-front` to wait for an external health check.
137. Create a PodDisruptionBudget for `store-front` with `minAvailable=2` for high availability.
138. Create a StatefulSet with a PersistentVolumeClaim template for 2Gi storage in `cassandra-db`.
139. Set up a headless service for the `cassandra-db` StatefulSet for direct pod access.
140. Create a Job with 10 completions and parallelism of 3 for batch processing.
141. Configure a CronJob with a concurrency policy of `Forbid` for `daily-report`.
142. Create a CronJob that runs every 15 minutes to clean up logs using `busybox`.
143. Set the `daily-report` CronJob to use the `UTC` time zone.
144. Configure the `daily-report` CronJob with a `successfulJobsHistoryLimit` of 3.
145. Create a deployment with pod affinity to co-locate with pods labeled `app=api` in `ecommerce`.
146. Set up pod anti-affinity for `store-front` to spread across availability zones.
147. Configure a deployment with a node selector `disktype=nvme` for high-performance storage.
148. Create a deployment with a toleration for `key=dedicated,value=app,effect=NoSchedule`.
149. Set resource requests (0.5 CPU, 512Mi memory) for the `store-front` deployment.
150. Configure liveness and readiness probes for `store-front` checking `/health` on port 80.
151. Create a deployment using environment variables from a ConfigMap named `store-config`.
152. Set up a deployment to use a Secret for database credentials in `ecommerce`.
153. Configure volume mounts from a ConfigMap for application settings in `store-front`.
154. Create a deployment with an init container to verify database connectivity.
155. Set up a sidecar container in `store-front` to forward logs to `/var/log/nginx`.
156. Configure an ambassador container in a deployment to proxy API requests.
157. Create a deployment with an adapter container to modify JSON responses.
158. Set up a multi-container pod in a deployment with `nginx` and `memcached`.
159. Configure a deployment with custom annotations for monitoring tools.
160. Create a deployment with a custom command `httpd -D FOREGROUND` for a web server.
161. Set an image pull policy of `Always` for a deployment to ensure fresh images.
162. Configure a deployment with a security context setting `runAsUser: 1001`.
163. Create a deployment with a PodSecurityPolicy enforcing non-privileged containers.
164. Set up a NetworkPolicy for `store-front` to restrict ingress to port 80.
165. Configure a service account named `store-sa` for a deployment in `ecommerce`.
166. Create a deployment with an RBAC Role allowing pod management in `payment`.
167. Set up pod priority for `store-front` with `priorityClassName: critical`.
168. Configure topology spread constraints for `store-front` across zones.
169. Create a deployment using a custom scheduler `app-scheduler`.
170. Set up a PodDisruptionBudget with `maxUnavailable=25%` for `store-front`.
171. Configure a HorizontalPodAutoscaler for `store-front` based on 70% memory usage.
172. Set up a VerticalPodAutoscaler with `updateMode: Auto` for `api-rs`.
173. Create a ResourceQuota for 6 CPU cores and 12Gi memory in the `inventory` namespace.
174. Configure a LimitRange for pods in the `payment` namespace with default limits.
175. Create a deployment with node affinity for `region=us-west` in `ecommerce`.
176. Set up pod anti-affinity for `cassandra-db` to ensure high availability.
177. Configure taints and tolerations for a deployment in the `prod` namespace.
178. Create a deployment using a specific StorageClass for persistent volumes.
179. Set up a PersistentVolumeClaim for a deployment in `inventory`.
180. Configure a ConfigMap for environment-specific settings in a deployment.
181. Create a Secret for API keys in a deployment in `payment`.
182. Set up environment variables from a Secret in `store-front`.
183. Configure volume mounts from a ConfigMap in `api-rs`.
184. Create a projected volume combining ConfigMap and Secret in a deployment.
185. Set up the downward API to expose pod metadata in `store-front`.
186. Configure a `hostPath` volume for logging in a deployment.
187. Create an `emptyDir` volume for caching in a deployment.
188. Set up an NFS volume for shared storage in a deployment.
189. Configure an AWS EBS volume for a database in a deployment.
190. Create a GCE PD volume for a deployment in `ecommerce`.

## Networking (191-260)

191. Create a ClusterIP service named `store-svc` for `store-front` on port 80.
192. Set up a NodePort service for `store-front` and access it from a node’s IP.
193. Create an Ingress resource to route `/shop` to the `store-svc` service in `ecommerce`.
194. Configure a NetworkPolicy in `ecommerce` to allow ingress to pods labeled `app=store` on port 80.
195. Create a manual Endpoint for a service without a selector pointing to `10.0.0.10:8080`.
196. Set up an IngressClass named `nginx-ingress` for the NGINX Ingress controller.
197. Create a LoadBalancer service for `store-front` in a cloud provider like AWS.
198. Configure a service with ports 80 (HTTP) and 443 (HTTPS) for `api-rs`.
199. Set up a headless service for `cassandra-db` to enable direct pod access.
200. Create a service with `externalName: db.external.com` for an external database.
201. Configure session affinity to `ClientIP` for the `store-svc` service.
202. Set up `externalTrafficPolicy: Local` for a LoadBalancer service.
203. Create an Ingress with TLS termination using a Secret named `tls-cert`.
204. Configure path-based routing in an Ingress for `/api` to `api-rs` and `/shop` to `store-svc`.
205. Set up host-based routing in an Ingress for `store.example.com`.
206. Create an Ingress with a rewrite rule to change `/oldshop` to `/shop`.
207. Configure a canary release in an Ingress using annotations for 10% traffic to a new version.
208. Set up rate limiting in an Ingress for `/api` using annotations.
209. Create a NetworkPolicy in `payment` to deny all ingress traffic to pods.
210. Configure a NetworkPolicy to allow traffic from the `ecommerce` namespace to `payment`.
211. Set up a NetworkPolicy for pod-to-pod communication within `inventory` on port 6379.
212. Create a NetworkPolicy to allow egress to an external payment gateway at `192.168.1.100`.
213. Configure a NetworkPolicy to allow TCP traffic on port 443 in `ecommerce`.
214. Set up a NetworkPolicy for communication between `ecommerce` and `payment` namespaces.
215. Create a service with a custom endpoint for an external Redis instance.
216. Configure CoreDNS to resolve services in the `ecommerce` namespace.
217. Set up CoreDNS with a custom upstream server for external DNS queries.
218. Install Kong API Gateway as a pod in the `ecommerce` namespace.
219. Configure Kong to route traffic to the `store-svc` service on `/shop`.
220. Set up Kong API Gateway to enforce rate limiting on `/api` endpoints.
221. Configure Kong to authenticate requests to `/payment` using API keys.
222. Create an Ingress with annotations to integrate with Kong API Gateway.
223. Set up a NetworkPolicy to allow egress to `api.stripe.com` from `payment`.
224. Configure a service with a health check endpoint `/healthz` for load balancing.
225. Set up readiness and liveness probes for a service’s pods checking `/status`.
226. Create a service with an external IP `192.168.1.200` assigned manually.
227. Configure RBAC to restrict network access for a service in `inventory`.
228. Set up a NetworkPolicy to allow traffic only from pods labeled `app=api` in `ecommerce`.
229. Create an Ingress with a default backend for unmatched paths pointing to `store-svc`.
230. Configure an IngressClass with parameters for the Traefik Ingress controller.
231. Set up a NetworkPolicy to allow ingress from CIDR `10.0.0.0/16` in `payment`.
232. Create a service with a session affinity timeout of 3600 seconds.
233. Configure a pod with a custom DNS resolver for `api.internal` in `ecommerce`.
234. Set up a pod with `hostNetwork: true` for a monitoring agent.
235. Create an Ingress with sticky sessions using cookie-based affinity.
236. Configure a service with `loadBalancerSourceRanges` to restrict access to `10.0.0.0/24`.
237. Set up a NetworkPolicy to deny all egress except to port 443 in `inventory`.
238. Create a pod with a `hostAliases` entry for `db.internal` resolving to `10.0.0.2`.
239. Configure an Ingress with a custom timeout of 60 seconds for long-running requests.
240. Set up a service with `externalTrafficPolicy: Cluster` for load balancing.
241. Create a NetworkPolicy to allow traffic between pods labeled `app=store` and `app=api`.
242. Configure an Ingress with path priority for `/shop` and `/shop/admin`.
243. Set up a service with a specific cluster IP `10.96.0.100`.
244. Create a pod with a DNS policy of `None` and custom search domains.
245. Configure an Ingress with a backend protocol of `GRPC` for a gRPC service.
246. Set up a NetworkPolicy to allow ingress from a specific pod in `ecommerce` to `payment`.
247. Create a service with a custom EndpointSlice for fine-grained control.
248. Configure a pod with a host port and a security context for a proxy.
249. Set up an Ingress with a path type of `Exact` for `/login`.
250. Create a NetworkPolicy to allow egress to `api.paypal.com` in `payment`.
251. Configure a service with a specific load balancer IP `192.168.1.201`.
252. Set up a pod with multiple network interfaces using Multus CNI.
253. Create an Ingress with a maximum request size limit of 5MB using annotations.
254. Configure a NetworkPolicy to deny all traffic except from CIDR `172.16.0.0/16`.
255. Set up a service with a health check node port for monitoring.
256. Create a pod with a custom hostname `frontend` and subdomain `app`.
257. Configure a NetworkPolicy to allow traffic to the `inventory` namespace only.
258. Set up an Ingress with multiple host rules for `store.example.com` and `api.example.com`.
259. Create a service with session stickiness using annotations.
260. Configure a pod with a static IP using a custom CNI plugin.

## Configuration (261-310)

261. Create a ConfigMap named `store-config` with keys `env=prod` and `log_level=debug` in `ecommerce`.
262. Mount the `store-config` ConfigMap as a volume at `/etc/config` in a pod.
263. Set environment variables in a pod from the `store-config` ConfigMap.
264. Create a Secret named `store-secret` with keys `api_key=abc123` and `db_pass=secret`.
265. Mount the `store-secret` Secret as a volume at `/etc/secrets` in a pod.
266. Use the `store-secret` Secret as environment variables in a pod.
267. Create a ConfigMap from a file `app.conf` with content `server=localhost`.
268. Create a Secret from a file `creds.txt` with content `token=xyz789`.
269. Update the `store-config` ConfigMap and verify pod configuration reload.
270. Rotate the `store-secret` Secret and update dependent pods.
271. Create a ConfigMap with multiple keys for a microservice’s settings in `payment`.
272. Mount a specific key `config.yaml` from `store-config` using `subPath` in a pod.
273. Create a Secret with a TLS certificate and key for the `store.example.com` domain.
274. Use the TLS Secret in an Ingress for secure routing to `store-svc`.
275. Create a ConfigMap with JSON data for an API configuration in `inventory`.
276. Inject JSON data from a ConfigMap as environment variables in a pod.
277. Create a Secret with Docker registry credentials for `docker.io/private`.
278. Use the Docker Secret to pull a private image in a pod in `ecommerce`.
279. Create a ConfigMap with binary data for a configuration file.
280. Mount the binary ConfigMap in a pod and verify its contents.
281. Use a ConfigMap to store a shell script and execute it in a pod.
282. Create a Secret with SSH keys for a Git repository access in `inventory`.
283. Use the SSH Secret in a pod to clone a private repository.
284. Configure a pod to hot-reload configuration from a ConfigMap for a web app.
285. Use the downward API to expose pod IP and namespace in a pod.
286. Expose pod annotations via the downward API in a pod for monitoring.
287. Create a projected volume combining `store-config` and `store-secret` in a pod.
288. Create a ConfigMap with a 2MB configuration file for a complex app.
289. Mount the large ConfigMap in a pod without causing memory issues.
290. Use a ConfigMap to store Java application properties in `payment`.
291. Inject ConfigMap data into a pod’s command-line arguments.
292. Create a Secret for OAuth tokens used by an API gateway in `ecommerce`.
293. Enable encryption at rest for Secrets in the cluster using a KMS provider.
294. Rotate the `store-secret` Secret and verify application continuity.
295. Integrate HashiCorp Vault to inject database credentials into a pod.
296. Configure Vault to manage Secrets for a payment processing app.
297. Set up RBAC to restrict access to ConfigMaps in the `inventory` namespace.
298. Enable audit logging to track access to Secrets in `payment`.
299. Use Kyverno to enforce a policy requiring specific keys in ConfigMaps.
300. Configure an admission webhook to validate ConfigMap data formats.
301. Create a ConfigMap from literal values `key1=value1` using `kubectl create configmap`.
302. Use a ConfigMap for multi-environment settings (prod, staging, dev) in `ecommerce`.
303. Manage configuration drift across environments using Kustomize overlays.
304. Create a Helm chart to manage ConfigMaps for the `store-front` deployment.
305. Parameterize a ConfigMap in a Helm template for reusable settings.
306. Create a ConfigMap for logging configuration in a microservice.
307. Mount a ConfigMap with `defaultMode: 0444` for read-only access in a pod.
308. Create a Secret with a client certificate for mutual TLS authentication.
309. Use a Secret to store environment-specific API keys in `payment`.
310. Configure a pod to use a ConfigMap for dynamic feature flags.

## Security (311-360)

311. Create a service account named `store-sa` in the `ecommerce` namespace.
312. Create a Role in `ecommerce` allowing `get` and `list` on pods and apply it.
313. Bind the Role from question 312 to `store-sa` using a RoleBinding.
314. Create a pod using `store-sa` and verify the service account is attached.
315. Configure a pod with a security context setting `runAsUser: 1000` in `payment`.
316. Set up a pod with `runAsNonRoot: true` for a web application.
317. Create a pod with `readOnlyRootFilesystem: true` for a stateless service.
318. Configure a pod with dropped capability `SYS_ADMIN` in `inventory`.
319. Create a ClusterRole allowing `list` on nodes across the cluster.
320. Bind the ClusterRole from question 319 to a user `admin-user` using a ClusterRoleBinding.
321. Configure a pod with `allowPrivilegeEscalation: false` for security.
322. Create a Secret with a service account token for API access in `ecommerce`.
323. Set up a Role in `payment` allowing `create` on ConfigMaps and bind it to `store-sa`.
324. Configure a pod with `fsGroup: 2000` for shared volume ownership.
325. Create a ClusterRole allowing `get` on services across the cluster.
326. Set up a pod with `capabilities.add: [NET_BIND_SERVICE]` for a proxy.
327. Create a RoleBinding in `inventory` to allow a user to delete pods.
328. Configure a pod with `seccompProfile: RuntimeDefault` for enhanced security.
329. Create a Role in `ecommerce` allowing `update` on deployments and bind it to `store-sa`.
330. Set up a pod with `capabilities.drop: [ALL]` to minimize privileges.
331. Create a ClusterRoleBinding to allow a service account to list PVs.
332. Configure a pod with `runAsGroup: 3000` in `payment`.
333. Create a Role in `inventory` allowing `list` on Secrets and bind it to a service account.
334. Set up a pod with `privileged: false` for a microservice.
335. Create a ClusterRole allowing `create` on namespaces across the cluster.
336. Configure a pod with `sysctls` to set `net.ipv4.ip_forward=1`.
337. Create a RoleBinding in `ecommerce` to allow a group to get pods.
338. Set up a pod with `fsGroupChangePolicy: OnRootMismatch` for volume management.
339. Create a Role in `payment` allowing `delete` on services and bind it to a service account.
340. Configure a pod with `runAsUser: 2000` and `runAsNonRoot: true`.
341. Create a ClusterRole allowing `list` on ConfigMaps across the cluster.
342. Set up a pod with `capabilities.add: [CHOWN]` for a specific task.
343. Create a RoleBinding in `inventory` to allow a user to update ConfigMaps.
344. Configure a pod with `seccompProfile: Unconfined` for a legacy app.
345. Create a ClusterRole allowing `delete` on nodes and bind it to a user.
346. Set up a pod with `readOnlyRootFilesystem: true` and `fsGroup: 4000`.
347. Create a Role in `ecommerce` allowing `get` on PVCs and bind it to a service account.
348. Configure a pod with `allowPrivilegeEscalation: false` and `capabilities.drop: [NET_RAW]`.
349. Create a ClusterRoleBinding to allow a group to list services.
350. Set up a pod with `runAsUser: 1001` and `runAsGroup: 1001` in `payment`.
351. Create a Role in `inventory` allowing `create` on deployments and bind it to a service account.
352. Configure a pod with `privileged: false` and `seccompProfile: RuntimeDefault`.
353. Create a ClusterRole allowing `get` on pods across the cluster.
354. Set up a pod with `capabilities.add: [SYS_TIME]` for a time-sensitive app.
355. Create a RoleBinding in `ecommerce` to allow a user to delete ConfigMaps.
356. Configure a pod with `fsGroup: 5000` and `runAsNonRoot: true`.
357. Create a Role in `payment` allowing `list` on services and bind it to a service account.
358. Set up a pod with `capabilities.drop: [SYS_PTRACE]` for security.
359. Create a ClusterRoleBinding to allow a service account to create ConfigMaps.
360. Configure a pod with `runAsUser: 3000` and `readOnlyRootFilesystem: true`.

## Storage (361-400)

361. Create a PersistentVolume (PV) with 5Gi capacity using NFS and mount it in a pod.
362. Create a PersistentVolumeClaim (PVC) requesting 2Gi in the `ecommerce` namespace.
363. Mount the PVC from question 362 in a pod for a database in `inventory`.
364. Create a StorageClass named `fast-storage` with provisioner `ebs.csi.aws.com`.
365. Configure a PVC to use the `fast-storage` StorageClass and verify dynamic provisioning.
366. Create a pod with an `emptyDir` volume for temporary cache data in `payment`.
367. Set up a `hostPath` volume in a pod for logging to `/var/log/app`.
368. Create a PV with a reclaim policy of `Retain` and bind it to a PVC.
369. Configure a pod to mount a ConfigMap as a volume for app settings.
370. Mount a Secret as a volume in a pod for database credentials.
371. Create a projected volume combining a ConfigMap and Secret in a pod.
372. Use the downward API to expose pod metadata as a volume in a pod.
373. Create a PVC with access mode `ReadWriteOnce` in `ecommerce`.
374. Configure a pod to mount an AWS EBS volume for persistent storage.
375. Set up a StorageClass with `reclaimPolicy: Delete` for dynamic provisioning.
376. Create a pod with a `hostPath` volume type `DirectoryOrCreate` in `inventory`.
377. Configure a PVC with a specific storage class name `fast-storage`.
378. Create a pod with an `emptyDir` volume using `medium: Memory`.
379. Mount a ConfigMap with `subPath: settings.yaml` in a pod.
380. Create a Secret with a Docker config JSON for a private registry.
381. Use the Docker Secret to pull a private image in a pod in `payment`.
382. Configure a PV with node affinity for specific storage nodes.
383. Create a pod with a volume mount for a Secret with `defaultMode: 0400`.
384. Set up a StorageClass with encryption parameters for secure storage.
385. Create a PVC with a selector to match a specific PV label.
386. Configure a pod to mount a projected volume with pod labels.
387. Create a ConfigMap with binary data and mount it in a pod.
388. Set up a Secret with type `Opaque` for custom credentials.
389. Create a PV with 10Gi capacity and a specific storage class.
390. Configure a pod to expose container limits via the downward API.
391. Set up a StorageClass with `volumeBindingMode: WaitForFirstConsumer`.
392. Create a PVC with access mode `ReadWriteMany` for shared storage.
393. Configure a pod to mount a ConfigMap with specific permissions.
394. Create a Secret with a TLS key pair and mount it in a pod.
395. Set up a PV with specific mount options for performance.
396. Configure a pod with an `emptyDir` volume with a size limit of 500Mi.
397. Create a ConfigMap with a large YAML file and mount it in a pod.
398. Set up a PVC with a specific storage request of 1Gi in `inventory`.
399. Configure a pod to mount a `hostPath` with a specific path type.
400. Create a Secret with multiple keys and use it as a projected volume.