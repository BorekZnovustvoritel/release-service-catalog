# custom-sbom pipeline

Tekton pipeline to generate and push component SBOMs for Snapshots.
This is a minimal pipeline derived from push-to-external-registry, containing only the
tasks necessary for collecting parameters and producing component SBOMs via the Mobster
augment-component-sboms task. It supports custom CA configuration at the pipeline level.

## Parameters

| Name                       | Description                                                                                            | Optional | Default value                                             |
|----------------------------|--------------------------------------------------------------------------------------------------------|----------|-----------------------------------------------------------|
| release                    | The namespaced name (namespace/name) of the Release custom resource initiating this pipeline execution | No       | -                                                         |
| releasePlan                | The namespaced name (namespace/name) of the releasePlan                                                | No       | -                                                         |
| releasePlanAdmission       | The namespaced name (namespace/name) of the releasePlanAdmission                                       | No       | -                                                         |
| releaseServiceConfig       | The namespaced name (namespace/name) of the releaseServiceConfig                                       | No       | -                                                         |
| snapshot                   | The namespaced name (namespace/name) of the snapshot                                                   | No       | -                                                         |
| taskGitUrl                 | The url to the git repo where the release-service-catalog tasks to be used are stored                  | Yes      | https://github.com/konflux-ci/release-service-catalog.git |
| taskGitRevision            | The revision in the taskGitUrl repo to be used                                                         | No       | -                                                         |
| ociStorage                 | The OCI repository where the Trusted Artifacts are stored                                              | Yes      | quay.io/konflux-ci/release-service-trusted-artifacts      |
| orasOptions                | oras options to pass to Trusted Artifacts calls                                                        | Yes      | ""                                                        |
| trustedArtifactsDebug      | Flag to enable debug logging in trusted artifacts. Set to a non-empty string to enable                 | Yes      | ""                                                        |
| dataDir                    | The location where data will be stored                                                                 | Yes      | /var/workdir/release                                      |
| mobster_tasks_git_revision | The git revision to be used when consuming Mobster tasks for SBOM processing                           | Yes      | updated-custom-ca                                         |
| conformaPubKey             | Path to the key used by Conforma to verify attestations signed by it                                   | Yes      | k8s://openshift-pipelines/public-key                      |
| caTrustConfigMapName       | The name of the ConfigMap to read CA bundle data from                                                  | Yes      | trusted-ca                                                |
| caTrustConfigMapKey        | The name of the key in the ConfigMap that contains the CA bundle data                                  | Yes      | ca-bundle.crt                                             |
| caCertPath                 | Path to CA certificate bundle for TLS verification with self-signed certificates                       | Yes      | /mnt/trusted-ca/ca-bundle.crt                             |
