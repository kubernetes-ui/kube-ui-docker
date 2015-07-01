# kube-ui-docker

This repo assumes that you've got https://github.com/kubernetes-ui/kube-ui cloned at the same level as this repo e.g.,
```
├── kube-ui-docker
├── kube-ui
```

To make the production code available to the Kubernetes api server, run this command from the top level directory:

```
hack/build-ui.sh dashboard
```

It runs the `go-bindata` tool to package the generated `app` directory and other user interface content, such as the Swagger documentation, into `pkg/ui/data/dashboard/datafile.go`. Note: go-bindata can be installed with `go get github.com/jteeuwen/go-bindata/...`.

Then, run `make kube-ui` in the `image` directory to build a new `kube-ui` binary that includes the updated `datafile.go`. When the updated UI is ready for release, increment the version tag in `image/Makefile` and run `make push` in the same directory to build & push the new kube-ui docker image.

### Serving the app in production
The app is served in production by the `kube-ui` binary at:

```
https://<kubernetes-master>/ui/
```

which redirects to:

```
https://<kubernetes-master>/api/v1/proxy/namespaces/default/services/kube-ui/
```
