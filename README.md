# Kubernetes Opdracht
Deze opdracht helpt je opweg met kubernetes. Daarnaast is de deployment van jullie groups project op het kubernetes cluster een verplicht onderdeel van de eindopdracht van het vak DevOps. Door deze opdracht wordt je geholpen om met kubernetes te werken. Dit helpt jullie direct het de deployment van jullie eigen project.

## Deel A: Zet Kubernetes aan via Docker Desktop
Om te beginnen met het gebruik van devops is het handig om kubernetes op je ontwikkel omgeving (laptop) op te zetten. Dit kan eenvoudig via Docker Desktop. (We gaan ervan uit dat jullie Docker in de voorgaande lessen al opgezet hebben). Volg de instructies uit de documentatie van Docker: [https://docs.docker.com/desktop/kubernetes/](https://docs.docker.com/desktop/kubernetes/)

Het verwachte eind resultaat van dit deel van de opdracht is dat Docker een lokale Kubernetes server heeft opgezet met een single-node cluster (je laptop). Hiermee kun je jouw kubernetes oplossing lokaal testen.

Daarnast zal je het commando `kubectl get nodes` in je terminal `docker-desktop` als node weergeven.

## Deel B: kubectl verbinden met het RPI-cluster
Je hebt nu je kubernetes voor je lokale ontwikkel omgeving opgezet en de kubectl tool in je terminal werkend. Nu Kunnen we kubectl laten verbinden met het RPI-cluster. Dit zodat kubectl tegen de kubernetes API praat ipv tegen die van je laptop.

Zorg dat je jouw `kubeconfig` file hebt gekregen van de docent. Hoe en waar je deze kunt krijgen zal worden uitgelegd tijdens de les. zie [voorbeeld_kubeconfig](voorbeeld_kubeconfig) hoe dit bestand eruit zou moeten zien.

Verplaatst dit bestand naar jouw `.kube` folder. Bijvoorbeeld 
```
mv [KUBECONFIG_LOCATIE] ~/.kube/kubeconfig_cluster.yaml
```


Zorg dat jouw terminal weet welke kubeconfig file het moet gebruiken bij het uitvoeren van kubectl commando's
```
export KUBECONFIG=~/.kube/kubeconfig_cluster.yaml
```

Iedere keer als je een terminal opnieuw opent dien je deze stap opnieuw uit te voeren.

Voor nu het volgende commando uit om te testen of je verbinding kunt maken met het cluster
```
kubectl get nodes
```
Als het goed is zie je nu meerder pi's onder elkaar weergegeven

Je hebt nu succesvol verbinding gemaakt met het cluster

## Deel C: Deploy jullie image naar het cluster
Nu is het doel om jullie om jullie docker image (die jullie in voorgaande lessen gepublished hebbben naar een docker registry zoals docker hub) te deployen.

Gebruik hiervoor [deploy.yml](deploy.yml) als voorbeeld. Pas dit bestand aan naar jullie situatie en gebruik het volgende commando op de deployment uit te voerne

`kubectl apply -f deploy.yml`

Het resultaat voor deze opdracht is dat jullie applicatie beschikbaar is via het volgende domein `https://[group_number].web.dops.tech`

## Deel D: Deployment in CI/CD pipeline
Zet nu jullie pipeline op om dmv jullie `kubeconfig` bestand, de `kubectl` tool en jullie `manifest` bestand. Zorg dat na het bouwen van jullie project het project gedeployed wordt.