# Image Apache/PHP pour TP Azure

L'image est construit à partir d'une image existante : https://hub.docker.com/r/webdevops/php-apache dont la documentation se trouve ici: https://dockerfile.readthedocs.io/en/latest/content/DockerImages/dockerfiles/php-apache.html


## Création et publication de l'image

```bash
# Se loguer a la registry créée sur Azure
docker login srault.azurecr.io

# Créer l'image à partir du Dockerfile local
docker build -t azure-tp:uat .

# Tester l'image : http://127.0.0.1:8081/
# ctrl-c dans le terminal pour sortir
docker run -it --rm -p 8081:80 azure-tp:uat

# Affecte un tag à l'image
docker tag azure-tp:uat srault.azurecr.io/azure-tp:uat

# Envoyer l'image dans la registry
docker push srault.azurecr.io/azure-tp:uat
```

## Le Dockerfile

```
FROM webdevops/php-apache:7.1-alpine

COPY index.php /app
```
