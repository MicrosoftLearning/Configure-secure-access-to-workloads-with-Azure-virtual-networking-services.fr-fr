---
lab:
  title: "Exercice\_: fournir l’isolation et la segmentation réseau pour l’application web"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---

# Labo : Fournir un réseau virtuel hub de services partagés avec isolement et segmentation

## Scénario

Vous avez été chargé d’appliquer des [principes de confiance zéro](https://learn.microsoft.com/security/zero-trust/azure-infrastructure-networking) à un réseau virtuel hub dans Azure. Le service informatique a besoin d’un isolement et d’une segmentation réseau pour l’application web dans un réseau spoke. Pour fournir un isolement et une segmentation réseau pour l’application web, vous devez créer un réseau virtuel Azure avec des sous-réseaux avec un espace d’adressage fourni par l’équipe informatique. Une fois le réseau virtuel créé, l’étape suivante consiste à configurer l’appairage de réseaux virtuels. Cela permet aux réseaux virtuels de communiquer entre eux en toute sécurité et en privé.

### Diagramme de l'architecture

![Diagramme montrant deux réseaux virtuels appairés.](../Media/task-1.png)

### Tâches d'apprentissage

- Créez un réseau virtuel
- Créer un sous-réseau
- Configurer VNET Peering

## Instructions de l’exercice

>**Remarque** : pour terminer ce labo, vous aurez besoin d’un [abonnement Azure](https://azure.microsoft.com/free/) avec le rôle RBAC **Contributeur** affecté.

> Dans ce labo, utilisez la valeur par défaut pour toutes les propriétés qui ne sont pas spécifiées quand vous êtes invité à créer une ressource.

### Créer des réseaux virtuels en étoile et des sous-réseaux

Commencez par créer les réseaux virtuels présentés dans le diagramme ci-dessus.

1. Connectez-vous au **portail Azure** - `https://portal.azure.com`.
   
1. Recherchez et sélectionnez `Virtual Networks`.
   
1. Sélectionnez **+ Créer** et effectuez la configuration du réseau **app-vnet**. Ce réseau virtuel nécessite deux sous-réseaux, **front-end** et **backend**. 

    | Propriété             | Valeur           |
    | :------------------- | :-------------- |
    | Groupe de ressources       | **RG1**         |
    | Nom du réseau virtuel | `app-vnet`    |
    | Région               | **USA Est**     |
    | Espace d’adressage IPv4   | **10.1.0.0/16** |
    | Nom du sous-réseau          | `frontend`    |
    | Plage d’adresses de sous-réseau | **10.1.0.0/24** |
    | Nom du sous-réseau          | `backend`     |
    | Plage d’adresses de sous-réseau | **10.1.1.0/24** |

    **Remarque** : laissez les autres paramètres avec leurs valeurs par défaut. Une fois terminé, sélectionnez **Examiner + créer**, puis **Créer**.
   
1. Créez la configuration du réseau virtuel **Hub-vnet**. Ce réseau virtuel comporte le sous-réseau de pare-feu. 

    | Propriété             | Valeur                    |
    | :------------------- | :----------------------- |
    | Groupe de ressources       | **RG1**                  |
    | Nom                 | `hub-vnet` |
    | Région               | **USA Est**              |
    | Espace d’adressage IPv4   | **10.0.0.0/16**          |
    | Nom du sous-réseau          | **AzureFirewallSubnet**  |
    | Plage d’adresses de sous-réseau | **10.0.0.0/24**          |

1. Une fois les déploiements terminés, recherchez et sélectionnez votre **groupe de ressources**. Vérifiez que vos nouveaux réseaux virtuels font partie du groupe de ressources. 

### Configurer une relation d’homologue entre les réseaux virtuels

1. Recherchez et sélectionnez le réseau virtuel `app-vnet`.
   
1. Sous **Paramètres**, sélectionnez **Peerings**.
   
1. Sélectionnez **+ Ajouter** pour ajouter un peering entre les deux réseaux virtuels. 

    | Propriété                                 | Valeur                          |
    | :--------------------------------------- | :----------------------------- |
    | Nom du lien de peering              | `app-vnet-to-hub` |
    | Réseau virtuel    | `hub-vnet` |
    | Nom du lien de peering de réseaux virtuels locaux | `hub-to-app-vnet` |

    **Remarque** : laissez les autres paramètres avec leurs valeurs par défaut. Sélectionnez **« Ajouter »** pour créer l’appairage de réseaux virtuels.

    [En savoir plus sur l’appairage de réseaux virtuels](https://learn.microsoft.com/azure/virtual-network/virtual-network-manage-peering?tabs=peering-portal)

1. Une fois le déploiement terminé, vérifiez que l’**état de peering** est **Connecté**. 
