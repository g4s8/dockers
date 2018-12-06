# PDD

Docker image with [pdd](https://github.com/yegor256/pdd/) installed,
can be used to validate pdd markers in container

## Examples

### CircleCI

Add to your `config.yml`:
```yaml
jobs:
  # ... skiped main jobs
  pdd-validator:
    docker:
      image: g4s8/pdd:alpine
    steps:
      - checkout
      - run: pdd --source=$(pwd) --verbose --file=/dev/null
workflow:
  version: 2
  build_and_test:
    jobs:
      # ... skiped jobs
      - pdd-validator
```
