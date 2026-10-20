## Construction d'une image à partir d'un Dockerfile

```shell
docker build -t <Nom-de-l-image> .
```
`docker build` : Lit un  `Dockefile` et exécute ses instruction une par une pour produire une image
`-t <nom>`: tag: donne un nom à l'image pour pouvoir la retrouver ensuite, on peut ajouter une version `-t frontend-docker:1.0`. Sans version, Docker met `:latest`
`.` : Le contexte de build : le dossier dont Docker peut copier les fichiers. Le point signifie "le dossier courant", le `Dockerfile` est cherché dans ce dossier.
## Création et lancement d'un conteneur à partir de l'image
```shell
docker run --name <nom-du-conteneur> -p 4242:xxxx <nom-de-l-image>
```

`docker run` : Crée un conteneur à partir d'une image et le démarre (c'est un  `create` + `start`)
`--name <nom>` : Nom du conteneur. Sans ça, Docker en invente un (ex: `quirky_turing`). Ce nom doit être unique.

`-p 4242:5173` : Publication de port, au format `port-hôte:port-conteneur`
`port-hôte` : le port de la machine par laquelle on accèdes à l'appli
`port-conteneur` : le port sur lequel Vite écoute dans le conteneur
`http://localhost:4242` : redirection vers le port 5173 du conteneur

`<nom-de-l-image>` : L'image à utiliser, ici celle construite à l'étape 1. Doit être le dernier arguments

`-d` : Mode détaché: le conteneur tourne en arrière-plan, le terminal reste libre

`--rm` : Supprime le conteneur automatiquement à son arrêt

`-it` : Mode interactif avec terminal

`--init` : Gère correctement les signaux d'arrêt

### Commandes associées

```shell
docker ps          # conteneurs en cours d'exécution
docker ps -a       # tous les conteneurs, même arrêtés
docker logs -f <nom>   # suivre les logs
docker stop <nom>      # arrêter proprement
docker rm <nom>        # supprimer un conteneur arrêté
docker rm -f <nom>     # forcer l'arrêt + suppression
docker images          # lister les images
```
