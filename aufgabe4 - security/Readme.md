# Security


## Lese Pods aus der API

```bash
oc rsh <pod>
cd /var/run/secrets/kubernetes.io/serviceaccount
token=$(cat token)
namespace=$(cat namespace)
curl -k "https://kubernetes.default.svc/api/v1/namespaces/${namespace}/pods"
curl -k -H "Authorization: Bearer ${token}" "https://kubernetes.default.svc/api/v1/namespaces/${namespace}/pods"
curl --cacert ca.crt -H "Authorization: Bearer ${token}" "https://kubernetes.default.svc/api/v1/namespaces/${namespace}/pods"
```

Wenn dein ServiceAccount keine Rechte hat, nutze
```bash
oc adm policy add-role-to-user view -z default -n <project-name>
```




## Aufgabe: User und Gruppen Ids

Vorbereitung:
```bash
oc apply -f prepare/
```

Doku: [PodSecurityContext](https://docs.openshift.com/container-platform/4.5/rest_api/objects/index.html#podsecuritycontext-core-v1)

Aufgabe: <br>
* Starte den Pod mit einer beliebigen, anderen User Id
* Setze eine eigene Gruppen Id
* Setze eine Gruppe als Dateisystem Gruppe (fgsGroup)
* Starte den Nutzer mit 3 zusätzlichen Gruppen


## Starte ein neues Deployment mit einem Apache Container

```bash
oc new-app library/httpd:stable
```

Untersuche warum der Container nicht startet.
