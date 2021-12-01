# Get Manifest file from Already created/running Kubernetes objects.

1. Manifest outputs are available at the `annotations` part of the `-o yaml` kubectl get cmds.
2. Those outputs are in JSON and you need to convert that into YAML.

3. For JSON to YAML conversion you need `yq`. 
Install `yq` from Github repo.
wget https://github.com/mikefarah/yq/releases/download/v4.15.1/yq_linux_amd64.tar.gz -O - | tar xz && mv yq_linux_amd64.tar.gz /usr/bin/yq
**note:** choose the version and binary based on your system. [YQ Github release page](https://github.com/mikefarah/yq/releases/)
4. Create the COPY the annotation's manifest part to a file.
5. Execute this cmd to get the YAML version of the manifest.
```
`yq e -P JSONFILENAME` or `cat JSONFILENAME | yq e -P -`

e or eval, Apply the expression to each document in each yaml file in sequence
-P or--prettyPrint, pretty print, shorthand for '... style = ""'
-, STDIN
```