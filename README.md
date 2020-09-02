你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# k8s-podinfo

Podinfo is a tiny web application made with Go 
that showcases best practices of running microservices in Kubernetes.

Specifications:

* Release automation (Make/TravisCI/CircleCI/Quay.io/Google Cloud Container Builder/Skaffold/Weave Flux)
* Multi-platform Docker image (amd64/arm/arm64/ppc64le/s390x)
* Health checks (readiness and liveness)
* Graceful shutdown on interrupt signals
* File watcher for secrets and configmaps
* Instrumented with Prometheus
* Tracing with Istio and Jaeger
* Structured logging with zap 
* 12-factor app with viper
* Fault injection (random errors and latency)
* Helm chart

Web API:

* `GET /` prints runtime information
* `GET /version` prints podinfo version and git commit hash 
* `GET /metrics` return HTTP requests duration and Go runtime metrics
* `GET /healthz` used by Kubernetes liveness probe
* `GET /readyz` used by Kubernetes readiness probe
* `POST /readyz/enable` signals the Kubernetes LB that this instance is ready to receive traffic
* `POST /readyz/disable` signals the Kubernetes LB to stop sending requests to this instance
* `GET /status/{code}` returns the status code
* `GET /panic` crashes the process with exit code 255
* `POST /echo` forwards the call to the backend service and echos the posted content 
* `GET /env` returns the environment variables as a JSON array
* `GET /headers` returns a JSON with the request HTTP headers
* `GET /delay/{seconds}` waits for the specified period
* `POST /token` issues a JWT token valid for one minute `JWT=$(curl -sd 'anon' podinfo:9898/token | jq -r .token)`
* `GET /token/validate` validates the JWT token `curl -H "Authorization: Bearer $JWT" podinfo:9898/token/validate`
* `GET /configs` returns a JSON with configmaps and/or secrets mounted in the `config` volume
* `POST /write` writes the posted content to disk at /data/hash and returns the SHA1 hash of the content
* `GET /read/{hash}` returns the content of the file /data/hash if exists
* `GET /ws/echo` echos content via websockets `podcli ws ws://localhost:9898/ws/echo`

### Guides

* [Deploy and upgrade with Helm](docs/1-deploy.md)
* [Horizontal Pod Auto-scaling](docs/2-autoscaling.md)
* [Monitoring and alerting with Prometheus](docs/3-monitoring.md)
* [StatefulSets with local persistent volumes](docs/4-statefulsets.md)
* [Expose Kubernetes services over HTTPS with Ngrok](docs/6-ngrok.md)
* [A/B Testing with Ambassador API Gateway](docs/5-canary.md)
* [Canary Deployments with Istio](docs/7-istio.md)
* [GitHub Actions CI demo](docs/8-gh-actions.md)
