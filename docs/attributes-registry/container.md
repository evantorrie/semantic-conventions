<!--- Hugo front matter used to generate the website version of this page:
--->

# Container

<!-- toc -->

- [Container Attributes](#container-attributes)
- [Deprecated Container Attributes](#deprecated-container-attributes)

<!-- tocstop -->

## Container Attributes

<!-- semconv registry.container(omit_requirement_level) -->
| Attribute  | Type | Description  | Examples  | Stability |
|---|---|---|---|---|
| `container.command` | string | The command used to run the container (i.e. the command name). [1] | `otelcontribcol` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.command_args` | string[] | All the command arguments (including the command/executable itself) run by the container. [2] | `[otelcontribcol, --config, config.yaml]` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.command_line` | string | The full command run by the container as a single string representing the full command. [2] | `otelcontribcol --config config.yaml` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.cpu.state` | string | The CPU state for this data point. | `user`; `kernel` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.id` | string | Container ID. Usually a UUID, as for example used to [identify Docker containers](https://docs.docker.com/engine/reference/run/#container-identification). The UUID might be abbreviated. | `a3bf90e006b2` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.image.id` | string | Runtime specific image identifier. Usually a hash algorithm followed by a UUID. [2] | `sha256:19c92d0a00d1b66d897bceaa7319bee0dd38a10a851c60bcec9474aa3f01e50f` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.image.name` | string | Name of the image the container was built on. | `gcr.io/opentelemetry/operator` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.image.repo_digests` | string[] | Repo digests of the container image as provided by the container runtime. [3] | `[example@sha256:afcc7f1ac1b49db317a7196c902e61c6c3c4607d63599ee1a82d702d249a0ccb, internal.registry.example.com:5000/example@sha256:b69959407d21e8a062e0416bf13405bb2b71ed7a84dde4158ebafacfa06f5578]` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.image.tags` | string[] | Container image tags. An example can be found in [Docker Image Inspect](https://docs.docker.com/engine/api/v1.43/#tag/Image/operation/ImageInspect). Should be only the `<tag>` section of the full name for example from `registry.example.com/my-org/my-image:<tag>`. | `[v1.27.1, 3.5.7-0]` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.label.<key>` | string | Container labels, `<key>` being the label name, the value being the label value. | `container.label.app=nginx` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.name` | string | Container name used by container runtime. | `opentelemetry-autoconf` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `container.runtime` | string | The container runtime managing this container. | `docker`; `containerd`; `rkt` | ![Experimental](https://img.shields.io/badge/-experimental-blue) |

**[1]:** If using embedded credentials or sensitive data, it is recommended to remove them to prevent potential leakage.

**[2]:** Docker defines a sha256 of the image id; `container.image.id` corresponds to the `Image` field from the Docker container inspect [API](https://docs.docker.com/engine/api/v1.43/#tag/Container/operation/ContainerInspect) endpoint.
K8s defines a link to the container registry repository with digest `"imageID": "registry.azurecr.io /namespace/service/dockerfile@sha256:bdeabd40c3a8a492eaf9e8e44d0ebbb84bac7ee25ac0cf8a7159d25f62555625"`.
The ID is assinged by the container runtime and can vary in different environments. Consider using `oci.manifest.digest` if it is important to identify the same image in different environments/runtimes.

**[3]:** [Docker](https://docs.docker.com/engine/api/v1.43/#tag/Image/operation/ImageInspect) and [CRI](https://github.com/kubernetes/cri-api/blob/c75ef5b473bbe2d0a4fc92f82235efd665ea8e9f/pkg/apis/runtime/v1/api.proto#L1237-L1238) report those under the `RepoDigests` field.

`container.cpu.state` has the following list of well-known values. If one of them applies, then the respective value MUST be used; otherwise, a custom value MAY be used.

| Value  | Description | Stability |
|---|---|---|
| `user` | When tasks of the cgroup are in user mode (Linux). When all container processes are in user mode (Windows). | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `system` | When CPU is used by the system (host OS) | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
| `kernel` | When tasks of the cgroup are in kernel mode (Linux). When all container processes are in kernel mode (Windows). | ![Experimental](https://img.shields.io/badge/-experimental-blue) |
<!-- endsemconv -->

## Deprecated Container Attributes

<!-- semconv registry.container.deprecated(omit_requirement_level) -->
| Attribute  | Type | Description  | Examples  | Stability |
|---|---|---|---|---|
| `container.labels.<key>` | string | Deprecated, use `container.label` instead. | `container.label.app=nginx` | ![Deprecated](https://img.shields.io/badge/-deprecated-red)<br>Replaced by `container.label`. |
<!-- endsemconv -->
