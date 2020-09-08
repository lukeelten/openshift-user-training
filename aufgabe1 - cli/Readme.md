# Command Line Interface

## Neues Projekt anlegen
```bash
oc new-project <name> --display-name "<display name>"
```

## Anlegen von Deployments
```bash
oc new-app lukeelten/openshift-nginx:stable
```

Man beachte, dass nicht nur das Deployment erstellt wird, sondern auch weitere Resourcen:
* Service (für die Ports die das Image exposed)
* ImageStream welches auf das original Image verweist

## Port forward in den Pod
```bash
oc get pods
oc port-forward --address 0.0.0.0 <pod-name> 8080:8080
```

Check if the pod serves any site on `http://<NUMBER>.work.cc-openshift.net:8080`

## Service von außen verfügbar machen
```bash
oc expose svc/openshift-nginx --port=8080
oc get route
```

Kopiere den Hostname der dort angezeigt wird in deinen Browser.


## Show Container Logs

```bash
oc logs <pod-name>
```

Container Logs sind der Output des Container Prozesses nach stdout und stderr. <br>
Kannst du deinen Aufruf von grade in den Logs finden?


## Automatisches Deployment kontrollieren
```bash
oc rollout pause deployment/<name>
oc rollout resume deployment/<name>
```

## Applikation restarten
```bash
oc rollout restart deployment/<name>
```
