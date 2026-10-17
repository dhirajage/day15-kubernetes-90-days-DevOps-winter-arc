# Day 15: Kubernetes Fundamentals (Kubeadm on AWS EC2)

## Objective
Deploy, scale, and expose a multi-replica Nginx application using declarative YAML manifests on a self-managed Kubernetes cluster built with Kubeadm on AWS EC2.

## Architecture & Key Concepts
- **Cluster:** The overall K8s environment running on AWS EC2.
- **Control Plane & Worker Nodes:** Managed via `kubeadm` init/join.
- **Pod:** The smallest deployable unit housing the Nginx container.
- **Deployment:** Ensures declarative desired state (managing 3 replicas and rolling updates).
- **Service (NodePort):** Exposes the application externally on port `30080`.

## Cluster Setup Verification
- Ran `kubectl get nodes` to ensure the EC2 node status is Ready.

## Deploy & Scale
- Applied `deployment.yaml` (started with 2 replicas).
- Applied `service.yaml` (configured NodePort `30080`).
- Scaled deployment to 3 replicas using `kubectl scale`.

## Troubleshooting Lessons Learned
- **EC2 Networking:** Ensured port `30080` was opened in the AWS EC2 Security Group inbound rules to successfully access the NodePort externally.
- **Pod Label Selectors:** Verified that Service endpoints mapped correctly using `kubectl get endpoints`.

## Cleanup
kubectl delete -f service.yaml
kubectl delete -f deployment.yaml
