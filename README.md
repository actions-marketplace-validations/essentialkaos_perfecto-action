<p align="center"><a href="#readme"><img src="https://gh.kaos.st/perfecto-action.svg"/></a></p>

<br/>

Action for checking RPM spec files with [_perfecto_](https://kaos.sh/perfecto).

### Usage

Create file `.github/workflows/perfecto.yml`.

Add next code to it:

```yml
name: CI

on:
  push:
    branches: [master, develop]
  pull_request:
    branches: [master]

jobs:
  Perfecto:
    name: Perfecto
    runs-on: ubuntu-latest

    steps:
      - name: Code checkout
        uses: actions/checkout@v3

      - name: Login to DockerHub
        uses: docker/login-action@v1
        env:
          DOCKERHUB_USERNAME: ${{ secrets.DOCKERHUB_USERNAME }}
        if: ${{ env.DOCKERHUB_USERNAME != '' }}
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Check specs with Perfecto
        uses: essentialkaos/perfecto-action@v1
        with:
          files: myapp.spec

```

### Options

- `files` - One or more files to check
- `format` - Output format (`summary`|`tiny`|`short`|`json`|`xml`)
- `error-level` - Return non-zero exit code if alert level greater than given (`notice`|`warning`|`error`|`critical`)
- `absolve` - Disable some checks by their ID ([wiki](https://kaos.sh/perfecto/w/Home))
- `image` - Name of official image of _perfecto_ (`tiny`|`centos7`)

### License

[Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)

<p align="center"><a href="https://essentialkaos.com"><img src="https://gh.kaos.st/ekgh.svg"/></a></p>
