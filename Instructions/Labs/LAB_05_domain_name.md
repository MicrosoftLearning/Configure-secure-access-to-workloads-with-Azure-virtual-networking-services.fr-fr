---
lab:
  title: "Exercice\_05\_: créer des zones DNS et configurer des paramètres DNS"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---

# Exercice 05 : créer des zones DNS et configurer des paramètres DNS

## Scénario

Votre organisation nécessite que les charges de travail utilisent des noms de domaine au lieu d’adresses IP pour les communications internes.  L’organisation ne souhaite pas ajouter de solution DNS personnalisée. Vous identifiez ces exigences.
+ Une **zone DNS privée** est nécessaire pour contoso.com.
+ Le DNS utilisera un **lien de réseau virtuel** vers le réseau app-vnet. 
+ Un nouvel **enregistrement DNS** est nécessaire pour le sous-réseau backend. 

## Tâches d'apprentissage

+ Créer et configurer une zone DNS privée.
+ Créez et configurez des enregistrements DNS.
+ Configurez les paramètres DNS sur un réseau virtuel.
  
## Diagramme de l'architecture

![Diagramme d’Azure DNS lié à un réseau virtuel.](../Media/task-5.png)



## Instructions de l’exercice

**Remarque :** cet exercice nécessite l’installation des réseaux virtuels et des sous-réseaux du Labo 01. Un [modèle](https://github.com/MicrosoftLearning/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/blob/main/Allfiles/Labs/All-Labs/create-vnet-subnets-template.json) est fourni si vous devez déployer ces ressources.

### Créer une zone DNS privée

Le [DNS privé Azure](https://learn.microsoft.com/azure/dns/private-dns-overview) fournit un service DNS fiable et sécurisé pour gérer et résoudre les noms de domaine dans un réseau virtuel sans nécessiter l’ajout de solution DNS personnalisée. Grâce aux zones DNS privées, vous pouvez utiliser vos propres noms de domaine personnalisés au lieu des noms fournis par Azure.

1. Dans le portail Azure, recherchez et sélectionnez `Private dns zones`.

1. Sélectionnez **+ Créer** et configurez la zone DNS. 

    | Propriété       | Valeur                        |
    | :------------- | :--------------------------- |
    | Abonnement   | **Sélectionnez votre abonnement** |
    | Resource group | **RG1**                      |
    | Nom           | `private.contoso.com`              |
    | Région         | **USA Est**                  |

1. Sélectionnez **Vérifier + créer**, puis sélectionnez **Créer**.

1. Attendez que la zone DNS soit déployée, puis sélectionnez **Accéder à la ressource**. 

### Créer une liaison de réseau virtuel vers votre zone DNS privée

Pour résoudre les enregistrements DNS dans une zone DNS privée, les ressources doivent être liées à la zone privée. Un [lien de réseau virtuel](https://learn.microsoft.com/azure/dns/private-dns-virtual-network-links) associe le réseau virtuel à la zone privée.

1. Dans le portail, continuez à travailler sur la zone DNS **private.contoso.com**. 

1. Dans le panneau **Gestion des DNS**, sélectionnez **+ Liens de réseau virtuel**.

1. Sélectionnez **+ Ajouter** et configurez le lien de réseau virtuel. 

    | Propriété                 | Valeur             |
    | :----------------------- | :---------------- |
    | Nom de la liaison                | `app-vnet-link` |
    | Réseau virtuel          | **app-vnet**      |
    | Activer l’inscription automatique | **Activé**       |

1. Sélectionnez **Créer** et attendez que le déploiement soit terminé. Si nécessaire, **actualisez** la page. 

### Créer un jeu d’enregistrements DNS

Les [enregistrements DNS](https://learn.microsoft.com/en-us/azure/dns/dns-zones-records#dns-records) fournissent des informations sur la zone DNS. 

1. Dans le portail, continuez à travailler sur la zone DNS **private.contoso.com**. 

1. Dans le panneau **Gestion des DNS**, sélectionnez **+ Recordsets**.

1. Notez que deux enregistrements A ont été créés automatiquement pour chacune des machines virtuelles. 

1. Sélectionnez **+ Ajouter** et configurez un jeu d’enregistrements. Lorsque vous avez terminé, sélectionnez **Ajouter**. 
   
    | Propriété   | Valeur        |
    | :--------- | :----------- |
    | Nom       | `backend`    |
    | Type       | **A**        |
    | TTL        | **1**        |
    | Adresse IP | **10.1.1.5** |

**Remarque :** ce jeu d’enregistrements implique qu’une machine virtuelle avec l’adresse IP privée 10.1.1.5 existe dans le réseau app-vnet.

### En savoir plus avec la formation en ligne

+ [Introduction à Azure DNS](https://learn.microsoft.com/training/modules/intro-to-azure-dns/). Ce module explique ce que fait Azure DNS, comment il fonctionne et quand choisir de l’utiliser comme solution pour répondre aux besoins de votre organisation.
+ [Héberger votre domaine sur Azure DNS](https://learn.microsoft.com/training/modules/host-domain-azure-dns/). Dans ce module, vous découvrez comment créer une zone DNS et des enregistrements DNS.

### Points clés

Félicitations ! Vous avez terminé l’exercice. Voici les points clés principaux :

+ Azure DNS est un service cloud qui vous permet d’héberger et de gérer des domaines DNS (Domain Name System), également appelés zones DNS. 
+ Les zones publiques Azure DNS hébergent les données de zone de nom de domaine pour les enregistrements que vous avez l’intention de résoudre par n’importe quel hôte sur Internet.
+ Les zones Azure DNS privé vous permettent de configurer un espace de noms de zone DNS privée pour les ressources Azure privées.
+ Une zone DNS est une collection d’enregistrements DNS. Les enregistrements DNS fournissent des informations sur le domaine.
