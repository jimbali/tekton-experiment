# Tekton experiment

This is a simple Tekton pipeline which will clone a Git repo, build a container
from the source code, and then push that container to Docker Hub.

## Requirements

- Tekton Pipelines
- Tekton `tkn` CLI tool

## Usage

Update `secrets.yaml` with your actual Docker creds ([see here](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/))

```
kubectl apply -f secret
```

Create the pipeline:

```
kubectl apply -f pipeline.yaml
```

Install pre-made tasks:

```
tkn hub install task git-clone
tkn hub install task kaniko
```

Run the pipeline:

```
kubectl create -f pipelinerun.yaml
```

It will print the name of the PipelineRun it created:

```
pipelinerun.tekton.dev/clone-build-push-run-bcv9f created
```

Tail the logs:

```
tkn pipelinerun logs  clone-build-push-run-4kgjr -f
```