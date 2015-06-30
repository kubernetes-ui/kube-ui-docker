# kube-ui-docker

To make the production code available to the Kubernetes api server, run this command from the top level directory:

```
hack/build-ui.sh dashboard
```

It runs the `go-bindata` tool to package the generated `app` directory and other user interface content, such as the Swagger documentation, into `pkg/ui/data/dashboard/datafile.go`. Note: go-bindata can be installed with `go get github.com/jteeuwen/go-bindata/...`.
