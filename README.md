# Image Apache/PHP pour TP Azure

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