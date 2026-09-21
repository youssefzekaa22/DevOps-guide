# 🎓 NEW Academy

A collection of complete, from-scratch-to-professional learning courses — written in Arabic, in a storytelling/dialogue style, and self-hosted using the exact same technologies they teach: **Docker** and **Kubernetes**.

Live demo: `http://z-academy.local` (or your configured Ingress host)

---

## 📚 Courses Included

| Course | File | Chapters | Topics |
|---|---|---|---|
| 🐧 Linux | `linux.html` | 25 | Commands, permissions, processes, system administration |
| 📚 Git | `git.html` | 13 | Branching, merging, rebase, remotes, workflows |
| 🌐 Networking | `networking.html` | 14 | OSI model, TCP/IP, subnetting, routing, DNS, firewalls, VPN |
| ☸️ Kubernetes Basics | `kubernetes.html` | 16 | Architecture, RBAC, Pod/Deployment/Service, Ingress, Helm |
| ⚙️ Kubernetes Advanced | `kubernetes-advanced.html` | 11 | DaemonSet, StatefulSet, HPA, NetworkPolicy, Operators, Monitoring, GitOps |

Each course includes:
- Dialogue-style explanations (learner ↔ mentor format)
- Real, runnable command examples
- Comparison tables and diagrams
- Collapsible Q&A sections for self-testing
- A full command/concept reference chapter

---

## 🏗️ Project Structure

```
zeeka-academy/
├── site/
│   ├── index.html                  # Landing page (course hub)
│   ├── linux.html
│   ├── git.html
│   ├── networking.html
│   ├── kubernetes.html
│   └── kubernetes-advanced.html
├── Dockerfile
├── deployment.yaml
├── service.yaml
├── ingress.yaml
└── README.md
```

---

## 🐳 Running Locally with Docker

### Build the image

```bash
docker build -t <your-dockerhub-username>/zeeka-academy:v1 .
```

### Run it

```bash
docker run -d -p 8080:80 --name zeeka-academy <your-dockerhub-username>/zeeka-academy:v1
```

Visit `http://localhost:8080`.

### Development mode (live edits with a bind mount)

```bash
docker run -d -p 8080:80 \
  -v $(pwd)/site:/usr/share/nginx/html \
  --name zeeka-academy <your-dockerhub-username>/zeeka-academy:v1
```

Any change inside `site/` appears immediately — no rebuild needed.

---

## ☸️ Deploying to Kubernetes

### 1. Push the image to a registry

```bash
docker push <your-dockerhub-username>/zeeka-academy:v1
```

### 2. Update the image name

Edit `deployment.yaml` and set the `image:` field to match what you pushed.

### 3. Apply the manifests

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
```

### 4. Point a hostname at your cluster

```bash
minikube ip   # or your cluster's external IP
```

Add the result to `/etc/hosts`:

```
<cluster-ip>   z-academy.local
```

### 5. Visit the site

```bash
curl http://z-academy.local
```

---

## 🔄 Updating the Site

Since the HTML files are baked into the image at build time, any change requires a new image and a rollout:

```bash
docker build -t <your-dockerhub-username>/zeeka-academy:v2 .
docker push <your-dockerhub-username>/zeeka-academy:v2
# update the image tag in deployment.yaml, then:
kubectl apply -f deployment.yaml
kubectl rollout status deployment/zeeka-academy
```

> Always use a new, distinct tag (`v2`, `v3`, ...) rather than reusing `latest` — Kubernetes may not pull an updated image if the tag hasn't changed.

---

## 🛠️ Tech Stack

- **Frontend:** Vanilla HTML/CSS/JavaScript — no framework, no build step
- **Web server:** nginx (alpine)
- **Containerization:** Docker
- **Orchestration:** Kubernetes (Deployment, Service, Ingress)
- **Fonts:** Google Fonts (Cairo, Tajawal, JetBrains Mono)

---

## 📄 License

Feel free to use, fork, and adapt for your own learning or teaching purposes.

---

## 🙏 Acknowledgments

Built as a hands-on learning project — every course here was written while learning the underlying technology (Docker, Kubernetes) that hosts it.
