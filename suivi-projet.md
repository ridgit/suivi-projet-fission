**Environnement Fission**

Qu’est-ce que fission, son architecture, ses composants de base, [consulter ce lien](https://fission.io/docs/architecture/) pour vous informer dessus

Comprendre comment [les requêtes http fonctionnent avec les fonctions Fission](https://fission.io/blog/demystifying-fission-http-requests-in-fission/)

**Installation de Fission**

**Conditions préalables :**

**1-**S’assurer d’avoir un cluster kubernetes et Helm déjà installé :

- [Lien d’installation d’un cluster kubernetes minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download#Ingress)
- [Lien d’installation de Helm](https://helm.sh/docs/intro/install/)

Vous allez sans doute avoir besoin de comprendre comment marche l’environnement kubernetes parce-que fission sera déployé dans un pod kubernetes, d’où lintérêt de comprendre les bases de comment fonction kubernetes.

Pour cela je vous invite à suivre ce [tutoriel youtube](https://www.youtube.com/watch?v=p3FsrSoFZ-Q&list=PLn6POgpklwWqfzaosSgX2XEKpse5VY2v5&index=4) qui est très bien structuré et vous permettra de vous y familiariser.

Passons à l’installation de fission

**2-**Pour ce faire on va utiliser helm en exécutant ces [commandes](https://fission.io/docs/installation/#install-fission)

**3**\-Installer par la suite [fission CLI](https://fission.io/docs/installation/#install-fission-cli) pour interagir avec fission

**4-**Vérifier que l’installation s’est bien effectuée à travers ces [commandes fission](https://fission.io/docs/installation/#verify-fission-installation)

**5-**[Deployer et exécuter](https://fission.io/docs/installation/#run-an-example) votre première fonction dans fission

**6-**Ce qu’on vient de faire est une installation standard de fission, cependant et ça sera certainement le cas, si vous souhaiter personnaliser l’installation de fission afin que cela se conforme à vos besoin, Helm nous vient en aide en utilisant le fichier [values.yaml](https://github.com/fission/fission-charts/blob/main/charts/fission-all/values.yaml) d’installation de fission.  
Voici ce que j'ai fait : 

```bash
helm repo add fission-charts https://fission.github.io/fission-charts/
helm repo update

export FISSION_NAMESPACE="fission"
kubectl create namespace $FISSION_NAMESPACE
kubectl create -k "github.com/fission/fission/crds/v1?ref=v1.20.2" # v1.20.2

# Télécharger le fichier values.yaml depuis le dépôt GitHub
curl -o values.yaml https://raw.githubusercontent.com/fission/fission-charts/main/charts/fission-all/values.yaml

# Modifier le fichier values.yaml selon vos besoins, si nécessaire

helm install fission --version v1.20.2 --namespace $FISSION_NAMESPACE -f values.yaml fission-charts/fission-all

#Install the client CLI on Linux
curl -Lo fission https://github.com/fission/fission/releases/download/v1.20.2/fission-v1.20.2-linux-amd64 && chmod +x fission && sudo mv fission /usr/local/bin/
#Tester que fission marche bien
fission version  
fission check

# .bashrc

# Auto-complétion pour Minikube
source <(minikube completion bash)

# Auto-complétion pour Fission
source <(fission completion bash)

# Auto-complétion pour kubectl
source <(kubectl completion bash)


```
Suivez ce process pour [**Déinstaller** fission](https://fission.io/docs/installation/uninstallation/) si le besoin se fait sentir.  
Je vous invite également à comprendre d’abord comment on peut [gérer les installations avec Helm](https://helm.sh/docs/chart_template_guide/getting_started/#charts).

Ce tutoriel [youtube](https://youtu.be/mcTwkE3jnZc?si=1A6NxN1EJvhyn6bu) est également très informative sur le sujet (personnaliser l’installation d’un chart avec Helm).

**Déploiement du dashboard kubernetes :**

Le dashboard kubernetes n'est pas déployée par défaut. Pour le déployer, [exécutez commande](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/#deploying-the-dashboard-ui)  

**Installation de terraform**  
```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

```
**#Etape 1 du projet : Utiliser terraform (IaC) pour déployer des fonctions sur fission**  
Prérequis :

    Un cluster Kubernetes opérationnel.
    Fission installé sur le cluster Kubernetes.
    Terraform installé sur votre machine de travail.
##-Terraform initialise un provider Kubernetes, crée un ConfigMap pour stocker le code de la fonction  
à faire..........  
##-déploie un pod en utilisant un Deployment qui utilise ce ConfigMap  

à faire..........  
##-génère une URL pour accéder à la fonction déployée.

à faire..........  
