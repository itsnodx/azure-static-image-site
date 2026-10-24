# Site statique Azure avec Azure Functions

## Description
Ce projet consiste à développer un site web statique hébergé sur Azure Blob Storage
qui interagit exclusivement avec des Azure Functions pour :

- Téléverser des images dans Azure Blob Storage
- Générer automatiquement des miniatures (256×256)
- Afficher les miniatures via une interface web statique

## Architecture
### Frontend
- HTML / CSS / JavaScript
- Hébergé via **Azure Blob Storage – Static Website**
- Aucune logique serveur côté client

### Backend (Azure Functions – Python)
1. **upload_image**  
   Fonction HTTP (POST)  
   Téléverse une image dans le conteneur `images-original`

2. **resize_image**  
   Fonction Blob Trigger  
   Redimensionne automatiquement l’image en 256×256 px à l’aide de la bibliothèque **Pillow (PIL)**  
   Stocke la miniature dans `images-thumbnails`

3. **list_images**  
   Fonction HTTP (GET)  
   Liste les miniatures disponibles et retourne leurs URLs publiques

### Stockage
- Azure Blob Storage
  - `images-original` : images sources
  - `images-thumbnails` : miniatures
---

---

##  Déploiement sur Azure

### Backend (Azure Functions)
```bash
cd functions
func azure functionapp publish func-static-image-site
```

### Frontend (Site statique)
```bash
cd frontend
az storage blob upload-batch   
 --account-name <STORAGE_ACCOUNT_NAME>   
 --destination '$web'   
 --source .   
 --overwrite
```

---

> Note : Le workflow GitHub Actions fourni illustre un déploiement CI/CD vers Azure Functions.
Les informations d’authentification Azure (Service Principal) ne sont pas incluses pour des raisons de sécurité.

---
 
## Technologies utilisées
- Azure Blob Storage
- Azure Functions (Python)
- Azure CLI
- Azure Functions Core Tools
- Pillow (PIL)
- HTML / CSS / JavaScript
- GitHub

---

## Ressources de déploiement

Les URL Azure de ce projet universitaire ne sont pas publiées ici, car elles peuvent avoir expiré ou avoir été désactivées. Utiliser les adresses fournies par son propre environnement Azure.
