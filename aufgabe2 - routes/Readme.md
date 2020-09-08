# Routes


## Vorbereitung

```bash
oc project <your-project>
oc apply -f deployment/
```

## Was passiert?

Es wird ein Deployment angelegt welches einen Nginx Pod startet. <br>
Zusätzlich wird ein Service angelegt der den HTTP und den HTTPS Port des Pods im Cluster erreichbar macht. <br>

Dann wird eine Route angelegt (wie vorhin mit `oc expose`) welche den Nginx außerhalb des Clusters erreichbar macht.

## Aufgabe

Erstelle Routen mit den verschiedenen TLS Terminiation Optionen und verbinde diese mit dem Service. <br>
Tipp: Achte auf die richtigen Ports!
