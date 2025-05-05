# helmfile 1.0.0 `toYaml` change

With helmfile `1.0.0` we get a schema validation error, as the string gets converted to integer.

```shell
❯ helmfile version

▓▓▓ helmfile

  Version            v1.0.0
  Git Commit         "brew"
  Build Date         27 Apr 25 18:57 CEST (1 week ago)
  Commit Date        27 Apr 25 18:57 CEST (1 week ago)
  Dirty Build        no
  Go version         1.24.2
  Compiler           gc
  Platform           linux/amd64
❯ helmfile template
Building dependency release=my-chart, chart=myChart
Templating release=my-chart, chart=myChart
in ./helmfile.yaml.gotmpl: command "/home/linuxbrew/.linuxbrew/bin/helm" exited with non-zero status:

PATH:
  /home/linuxbrew/.linuxbrew/bin/helm

ARGS:
  0: helm (4 bytes)
  1: template (8 bytes)
  2: my-chart (8 bytes)
  3: myChart (7 bytes)
  4: --values (8 bytes)
  5: /tmp/helmfile4267302090/my-chart-values-dc67888f9 (49 bytes)

ERROR:
  exit status 1

EXIT STATUS
  1

STDERR:
  Error: values don't meet the specifications of the schema(s) in the following chart(s):
  myChart:
  - thisShouldBeString: Invalid type. Expected: string, given: integer

COMBINED OUTPUT:
  Error: values don't meet the specifications of the schema(s) in the following chart(s):
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
