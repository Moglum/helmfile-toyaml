# helmfile 1.0.0 `toYaml` change

Related helmfile issue <https://github.com/helmfile/helmfile/issues/2024>

## To reproduce

Helmfile `1.0.0` returna a validation error, as the string gets converted to integer.

```shell
❯ helmfile template --debug
processing file "helmfile.yaml" in directory "."
changing working directory to "/home/moglum/tmp/helmfile-int-bug"
envvals_loader: loaded defaults.yaml:map[thisShouldBeString:01234567890123456789]
merged environment: &{default  map[thisShouldBeString:01234567890123456789] map[]}
merged environment: &{default  map[thisShouldBeString:01234567890123456789] map[]}
helm:YcSkz> v3.17.3+ge4da497
helm:YcSkz>
Building dependency release=my-chart, chart=myChart
exec: helm dependency build myChart
1 release(s) found in helmfile.yaml

processing 1 groups of releases in this order:
GROUP RELEASES
1     my-chart

processing releases in group 1/1: my-chart
Successfully generated the value file at myChart/values.yaml.gotmpl. produced:
thisShouldBeString: 01234567890123456789


Templating release=my-chart, chart=myChart
exec: helm template my-chart myChart --values /tmp/helmfile2967871048/my-chart-values-5d96b755fb --debug
helm:ePUGM> install.go:225: 2025-05-05 12:43:07.108430572 +0200 CEST m=+0.040911209 [debug] Original chart version: ""
helm:ePUGM> install.go:242: 2025-05-05 12:43:07.108498339 +0200 CEST m=+0.040978974 [debug] CHART PATH: /home/moglum/tmp/helmfile-int-bug/myChart
helm:ePUGM>
helm:ePUGM>
helm:ePUGM> Error: values don't meet the specifications of the schema(s) in the following chart(s):
helm:ePUGM> myChart:
helm:ePUGM> - thisShouldBeString: Invalid type. Expected: string, given: integer
helm:ePUGM>
helm:ePUGM> helm.go:86: 2025-05-05 12:43:07.125746022 +0200 CEST m=+0.058226672 [debug] values don't meet the specifications of the schema(s) in the following chart(s):
helm:ePUGM> myChart:
helm:ePUGM> - thisShouldBeString: Invalid type. Expected: string, given: integer
helm:ePUGM>
helm:ePUGM>
Removed /tmp/helmfile2967871048/my-chart-values-5d96b755fb
Removed /tmp/helmfile2967871048
err: command "/home/linuxbrew/.linuxbrew/bin/helm" exited with non-zero status:

PATH:
  /home/linuxbrew/.linuxbrew/bin/helm

ARGS:
  0: helm (4 bytes)
  1: template (8 bytes)
  2: my-chart (8 bytes)
  3: myChart (7 bytes)
  4: --values (8 bytes)
  5: /tmp/helmfile2967871048/my-chart-values-5d96b755fb (50 bytes)
  6: --debug (7 bytes)

ERROR:
  exit status 1

EXIT STATUS
  1

STDERR:
  install.go:225: 2025-05-05 12:43:07.108430572 +0200 CEST m=+0.040911209 [debug] Original chart version: ""
  install.go:242: 2025-05-05 12:43:07.108498339 +0200 CEST m=+0.040978974 [debug] CHART PATH: /home/moglum/tmp/helmfile-int-bug/myChart
  Error: values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer
  helm.go:86: 2025-05-05 12:43:07.125746022 +0200 CEST m=+0.058226672 [debug] values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer

COMBINED OUTPUT:
  install.go:225: 2025-05-05 12:43:07.108430572 +0200 CEST m=+0.040911209 [debug] Original chart version: ""
  install.go:242: 2025-05-05 12:43:07.108498339 +0200 CEST m=+0.040978974 [debug] CHART PATH: /home/moglum/tmp/helmfile-int-bug/myChart
  Error: values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer
  helm.go:86: 2025-05-05 12:43:07.125746022 +0200 CEST m=+0.058226672 [debug] values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer
changing working directory back to "/home/moglum/tmp/helmfile-int-bug"
in ./helmfile.yaml: command "/home/linuxbrew/.linuxbrew/bin/helm" exited with non-zero status:

PATH:
  /home/linuxbrew/.linuxbrew/bin/helm

ARGS:
  0: helm (4 bytes)
  1: template (8 bytes)
  2: my-chart (8 bytes)
  3: myChart (7 bytes)
  4: --values (8 bytes)
  5: /tmp/helmfile2967871048/my-chart-values-5d96b755fb (50 bytes)
  6: --debug (7 bytes)

ERROR:
  exit status 1

EXIT STATUS
  1

STDERR:
  install.go:225: 2025-05-05 12:43:07.108430572 +0200 CEST m=+0.040911209 [debug] Original chart version: ""
  install.go:242: 2025-05-05 12:43:07.108498339 +0200 CEST m=+0.040978974 [debug] CHART PATH: /home/moglum/tmp/helmfile-int-bug/myChart
  Error: values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer
  helm.go:86: 2025-05-05 12:43:07.125746022 +0200 CEST m=+0.058226672 [debug] values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer

COMBINED OUTPUT:
  install.go:225: 2025-05-05 12:43:07.108430572 +0200 CEST m=+0.040911209 [debug] Original chart version: ""
  install.go:242: 2025-05-05 12:43:07.108498339 +0200 CEST m=+0.040978974 [debug] CHART PATH: /home/moglum/tmp/helmfile-int-bug/myChart
  Error: values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer
  helm.go:86: 2025-05-05 12:43:07.125746022 +0200 CEST m=+0.058226672 [debug] values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer 
```

When using older helmfile `0.171.0` it works as expected

```shell
❯ ./helmfile_0.171.0_linux_amd64 version

▓▓▓ ./helmfile_0.171.0_linux_amd64

  Version            0.171.0
  Git Commit         41d8070
  Build Date         12 Feb 25 09:45 CET (2 months ago)
  Commit Date        12 Feb 25 07:31 CET (2 months ago)
  Dirty Build        no
  Go version         1.23.1
  Compiler           gc
  Platform           linux/amd64

  │ A new release is available: 0.171.0 → v1.0.0
  │ https://github.com/helmfile/helmfile/releases/tag/v1.0.0
❯ ./helmfile_0.171.0_linux_amd64 template
Building dependency release=my-chart, chart=myChart
Templating release=my-chart, chart=myChart
---
# Source: myChart/templates/values.yaml
thisShouldBeString: "01234567890123456789"
```
