# GitHub Spec minify reproducer
A reproducer for failure to minify GitHub spec file.

## Prerequisite
Having `kn-workflow` 1.35 cli [installed](https://mirror.openshift.com/pub/cgw/serverless-logic/1.35.0/).

```bash
kn-workflow version
Version: 1.35.0

Default Quarkus version:           3.8.6.SP2-redhat-00002
Default Quarkus platform group Id: com.redhat.quarkus.platform
Kogito Version: 9.102.0.redhat-00005
DevMode Image: registry.redhat.io/openshift-serverless-1/logic-swf-devmode-rhel8:1.35.0
```

## Steps to reproduce

To reproduce the failure to minify GitHub spec file, run the following commands:
```bash
git clone git@github.com:masayag/gh-specs-minify-reproducer.git
cd gh-specs-minify-reproducer
kn-workflow specs minify openapi
```

Result:
```bash
Error: ❌ ERROR: Minification of /home/masayag/junk/gh-specs-minify/specs/github.yaml failed: ❌ ERROR: Minified file /home/masayag/junk/gh-specs-minify/specs/github.min.yaml exceeds the size limit of 3145728 bytes
Usage:
  kn workflow specs minify openapi [flags]

Examples:

	#Minify the workflow project's OpenAPI spec file located in the current project.
	{{.Name}} specs minify openapi

	# Specify a custom subflows files directory. (default: ./subflows)
	{{.Name}} specs minify openapi --subflows-dir=<full_directory_path>

	# Specify a custom support specs directory. (default: ./specs)
	{{.Name}} specs minify openapi --specs-dir=<full_directory_path>
		

Flags:
  -h, --help                  help for openapi
  -p, --specs-dir string      Specify a custom specs files directory
  -s, --subflows-dir string   Specify a custom subflows files directory

❌ ERROR: Minification of /home/masayag/junk/gh-specs-minify/specs/github.yaml failed: ❌ ERROR: Minified file /home/masayag/junk/gh-specs-minify/specs/github.min.yaml exceeds the size limit of 3145728 bytes
```
 and a generated spec file (size > 6M):
```
→ ll -h specs/github.min.yaml
-rw-r--r--. 1 masayag masayag 6.3M Feb 16 15:13 specs/github.min.yaml
```

