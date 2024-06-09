# ec2-docker-service-deploy-action

EC2 Docker service deploy and optional in-action security group ip whitelisting

## Usage

```yaml
name: ci

on:
  push:

jobs:
  qemu:
    runs-on: ubuntu-latest
    steps:
      - name: Docker QEMU Buildx ECR
        uses: bbharathkumarreddy/ec2-docker-service-deploy-action@v1.0
        with:
          ssh-host: ${{ vars.ssh-host }}
          ssh-key: ${{ secrets.ssh-key }}
          aws-access-key-id: ${{ secrets.aws-access-key-id }}
          aws-secret-access-key: ${{ secrets.aws-secret-access-key }}
          aws-region: ${{ vars.aws-region }}
          security-group-id: ${{ vars.aws-security-group-id }}
          ecr-image-uri: ${{ vars.ecr-uri }}
          docker-service: my-service
          replicas: 2
          docker-network: my-network
          docker-published-port: 80
          docker-target-port: 80
```

## Customizing

### inputs

The following inputs can be used as `step.with` keys:

| Name                    | Type    | Default      | Description                                                                                                                                  |
| ----------------------- | ------- | ------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `ssh-host`              | String  |              | SSH hostname or ip address.                                                                                                                  |
| `ssh-key`               | String  |              | SSH key to connect to host machine.                                                                                                          |
| `ssh-port`              | String  | `22`         | SSH port to deploy the service.                                                                                                              |
| `ssh-username`          | String  | `ec2-user`   | SSH username.                                                                                                                                |
| `aws-access-key-id`     | String  |              | Pass the AWS access key id.                                                                                                                  |
| `aws-secret-access-key` | String  |              | Pass the AWS secret access key.                                                                                                              |
| `aws-region`            | String  |              | Pass the AWS region.                                                                                                                         |
| `security-group-id:`    | String  |              | AWS security group id to whitelist github action's ip address temporarily.                                                                   |
| `ecr-image-uri`         | String  |              | ECR Container image URI with tag.                                                                                                            |
| `docker-service`        | String  | `my-service` | Docker service name.                                                                                                                         |
| `replicas`              | String  | `1`          | Number of service replicas.                                                                                                                  |
| `docker-network`        | String  | `ingress`    | Docker network.                                                                                                                              |
| `docker-published-port` | String  | `80`         | Docker port to publish.                                                                                                                      |
| `docker-target-port`    | String  | `80`         | Docker target port of container.                                                                                                             |
| `docker-opts`           | String  |              | More docker options to create docker service. eg. `--log-driver=awslogs --log-opt awslogs-group=my-logs --log-opt awslogs-region=us-east-1`. |
| `prune`                 | Boolean | `true`       | On prune true, Will cleanup exitied containers and unused images.                                                                            |
| `restart-only`          | Boolean | `false`      | On restart-only true, Service will be force restarted with set replicas.                                                                       |

## Contributing

Want to contribute? ✅
