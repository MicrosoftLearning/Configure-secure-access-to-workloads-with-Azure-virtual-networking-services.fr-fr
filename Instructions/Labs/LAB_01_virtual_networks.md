---
lab:
  title: "Exercice\_: fournir l’isolation et la segmentation réseau pour l’application web"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---

# Labo : fournir l’isolation et la segmentation réseau pour l’application web

## Scénario

Le service informatique a besoin d’une isolation et d’une segmentation réseau pour l’application web. Pour fournir une isolation et une segmentation réseau pour l’application web, vous devez créer un réseau virtuel Azure avec des sous-réseaux fournis par l’équipe informatique. Une fois le réseau virtuel créé, l’étape suivante consiste à configurer l’appairage de réseaux virtuels. Cela permet aux réseaux virtuels de communiquer entre eux en toute sécurité et en privé.

### Diagramme de l'architecture

![Diagramme montrant deux réseaux virtuels appairés.](../Media/task-1.png)

### Tâches d'apprentissage

- Créez un réseau virtuel
- Créer un sous-réseau
- Configurer VNET Peering

## Instructions de l’exercice

>**Remarque** : pour terminer ce labo, vous aurez besoin d’un [abonnement Azure](https://azure.microsoft.com/free/) avec le rôle RBAC **Contributeur** affecté.
> Dans ce labo, utilisez la valeur par défaut pour toutes les propriétés qui ne sont pas spécifiées quand vous êtes invité à créer une ressource.

### Créer des réseaux et des sous-réseaux virtuels

Commencez par créer les réseaux indiqués dans le diagramme ci-dessus.

1. Ouvrez un navigateur, accédez au <a href="https://portal.azure.com/#home">portail Microsoft Azure</a> et connectez-vous.
1. Pour créer un réseau virtuel, dans la barre de recherche en haut du portail, saisissez **« Réseau virtuel »** et sélectionnez **« Réseaux virtuels »** dans les résultats.
1. Dans le volet du portail **« Réseaux virtuels »**, sélectionnez «  **+ Créer** ».
1. Remplissez tous les onglets du processus de création à l’aide des valeurs du tableau suivant :

    | Propriété             | Valeur           |
    | :------------------- | :-------------- |
    | Groupe de ressources       | **RG1**         |
    | Nom                 | **app-vnet**    |
    | Région               | **USA Est**     |
    | Espace d’adressage IPv4   | **10.1.0.0/16** |
    | Nom du sous-réseau          | **frontend**    |
    | Plage d’adresses de sous-réseau | **10.1.0.0/24** |
    | Nom du sous-réseau          | **serveur principal**     |
    | Plage d’adresses de sous-réseau | **10.1.1.0/24** |

    **Remarque** : laissez les autres paramètres avec leurs valeurs par défaut. Sélectionnez **« Suivant »** pour passer à l’onglet suivant, puis **Créer** pour créer le réseau virtuel.
1. En suivant la même procédure que ci-dessus, créez le réseau virtuel Azure **shared-services-vnet** en utilisant les valeurs indiquées dans le tableau suivant :

    | Propriété             | Valeur                    |
    | :------------------- | :----------------------- |
    | Groupe de ressources       | **RG1**                  |
    | Nom                 | **shared-services-vnet** |
    | Région               | **USA Est**              |
    | Espace d’adressage IPv4   | **10.0.0.0/16**          |
    | Nom du sous-réseau          | **frontend**             |
    | Plage d’adresses de sous-réseau | **10.0.0.0/24**          |

1. Une fois le déploiement terminé : Revenez au portail, dans la barre de recherche, saisissez **« groupes de ressources »**, puis sélectionnez **« Groupes de ressources »** dans les résultats. Sélectionnez **« RG1 »** dans le volet principal et confirmez que les deux réseaux virtuels ont été déployés.

### Configurer une relation d’homologue entre les réseaux virtuels

1. Configurez une relation d’homologue entre les réseaux virtuels pour permettre au trafic de transiter dans les deux sens entre les réseaux virtuels **app-vnet** et **shared-services-vnet**.
1. Dans le portail, dans la vue du groupe de ressources RG1. Sélectionnez le réseau virtuel **« app-vnet »**.
1. Dans le menu contextuel **app-vnet** sur le côté gauche du portail, faites défiler l’écran vers le bas et sélectionnez **peerings**
1. Dans le volet de peerings **app-vnet**, sélectionnez **+ Ajouter**.
1. Remplissez le formulaire en utilisant les valeurs contenues dans le tableau suivant :

    | Propriété                                 | Valeur                          |
    | :--------------------------------------- | :----------------------------- |
    | Nom de cette liaison d’appairage de réseaux virtuels   | **app-vnet-to-sharedservices** |
    | Nom de cette liaison d’appairage de réseaux virtuels distants | **sharedservices-to-app-vnet** |
    | Réseau virtuel                          | **shared-services-vnet**       |

    **Remarque** : laissez les autres paramètres avec leurs valeurs par défaut. Sélectionnez **« Ajouter »** pour créer l’appairage de réseaux virtuels.

    [En savoir plus sur l’appairage de réseaux virtuels](https://learn.microsoft.com/azure/virtual-network/virtual-network-manage-peering?tabs=peering-portal)

1. Une fois le processus terminé, et après la mise à jour de la configuration : Vérifiez que **l’état du peering** est défini sur **Connecté**. (vous devrez peut-être actualiser la page pour voir l’état mis à jour)
