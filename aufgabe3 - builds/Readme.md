# ImageStreams


## Anlegen eines ImageStreams

```bash
# Erstellen des ImageStream
oc create imagestream test
# Auflisten der Imagestreams
oc get imagestream
oc get is
## ImagestreamTags sind konkrete Images mit Tags
oc get imagestreamtag
oc get istag
```

## Importieren externer Images

```bash
#oc import-image <name>:<tag> --from=<registry>/<image>:<tag> [--confirm] [--reference-policy=local] [--scheduled]
oc import-image apache:latest --from=docker.io/library/httpd:latest --confirm
oc import-image ubi:8 --from=registry.access.redhat.com/ubi8/ubi:latest --scheduled --confirm --reference-policy=local
```

## Lookup Policy

ImageStream haben eine Option namens "lookup policy". Diese bestimmt ob dieses Image nur mittels vollständiger Url verfügbar ist, oder ob es in den Suchpfad mit aufgenommen wird.

```bash
oc apply -f deployment.yaml
oc get pod
# Pod startet nicht weil er das image nicht finden kann
# Eigentlich hatten wir grade ein Image namens ubi:8 importiert
oc scale deployment/imagestream-test --replicas=0
oc patch is ubi --type=merge -p '{"spec": {"lookupPolicy": {"local": true}}}'
oc scale deployment/imagestream-test --replicas=1
```

# Builds

## Erstellen eines eigenen Images

1. Suche ein offences Github Repository mit Dockerfile
2. Erstelle einen ImageStream 
3. Erstelle eine BuildConfig die daraus ein Image baut

Beispiel Repository: https://github.com/lukeelten/nginx-example.git

