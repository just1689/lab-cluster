# Creating

## Installing Loki 
Install by running the following command in this directory

```shell
kubectl apply -f .
```

## Original Source

This was created using the following commands

```shell script
helm template loki -n loki-stack --set fluent-bit.enabled=true,promtail.enabled=true,loki.persistence.enabled=true,loki.persistence.size=10Gi --namespace=loki-stack loki/loki-stack > 01-stack.yaml 

```

I've removed the Secret and moving it to secret.yaml and remove the last line. See changing config below.


## Changing the Loki config

The file `00-config-for-secret.yaml.txt` is the plain text version of what becomes `02-secret.yaml`. 
Once you modify the file `00-config-for-secret.yaml.txt` run the following command: 

```shell
sed -i '$ d' 02-secret.yaml && echo "  loki.yaml: $( cat 00-config-for-secret.yaml.txt | base64 -w 0 )" >> 02-secret.yaml
```


