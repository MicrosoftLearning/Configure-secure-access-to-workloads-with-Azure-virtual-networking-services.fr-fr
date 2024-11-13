---
lab:
  title: "Exercice\_02\_: créer et configurer des groupes de sécurité réseau"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---

# Exercice 02 : créer et configurer des groupes de sécurité réseau

## Scénario

Votre organisation nécessite le contrôle du trafic réseau en direction et en provenance du réseau app-vnet. Vous identifiez ces exigences.
+ Le sous-réseau frontend comprend des serveurs Web accessibles à partir d’Internet. Un **groupe de sécurité des applications **(ASG) est nécessaire pour ces serveurs. L’ASG doit être associé à n’importe quelle interface de machine virtuelle qui fait partie du groupe. Cela permettra de gérer facilement les serveurs Web. 
+ Une **règle NSG** est nécessaire pour autoriser le trafic HTTPS entrant vers l’ASG. Cette règle utilise le protocole TCP sur le port 443. 
+ Le sous-réseau backend comprend des serveurs de base de données utilisés par les serveurs Web frontend. Un **groupe de sécurité réseau** (NSG) est nécessaire pour contrôler ce trafic. Le NSG doit être associé à n’importe quelle interface de machine virtuelle accessible par les serveurs Web. 
+ Une **règle NSG** est nécessaire pour autoriser le trafic réseau entrant de l’ASG vers les serveurs backend.  Cette règle utilise le service MS SQL et le port 1443. 
+ Pour les tests, une machine virtuelle doit être installée dans le sous-réseau frontend (VM1) et le sous-réseau backend (VM2).  Le groupe informatique a fourni un modèle Azure Resource Manager pour déployer ces **serveurs Ubuntu**. 

## Tâches d'apprentissage

+ Créer des groupes de sécurité réseau
+ Créer des règles de groupe de sécurité réseau.
+ Associer un groupe de sécurité réseau à un sous-réseau.
+ Créer et utiliser des groupes de sécurité des applications dans des règles de groupe de sécurité réseau.

## Diagramme de l'architecture

![Diagramme montrant un groupe de sécurité réseau et un groupe de sécurité d’application associés à un réseau virtuel.](../Media/task-2.png)




## Instructions de l’exercice

### Créer l’infrastructure réseau pour l’exercice

**Remarque :** cet exercice nécessite l’installation des réseaux virtuels et des sous-réseaux du Labo 01. Un [modèle](https://github.com/MicrosoftLearning/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/blob/main/Allfiles/Labs/All-Labs/create-vnet-subnets-template.json) est fourni si vous devez déployer ces ressources.

1. Utilisez l’icône (en haut à droite) pour lancer une session **Cloud Shell**. Vous pouvez également directement accéder à `https://shell.azure.com`.

1. Lorsque vous êtes invité à sélectionner **Bash** ou **PowerShell**, sélectionnez **PowerShell**.

1. Le stockage n’est pas nécessaire pour cette tâche. Sélectionnez votre abonnement. 

1. Déployez les machines virtuelles nécessaires pour cet exercice. 

   ```powershell
   $RGName = "RG1"
   
   New-AzResourceGroupDeployment -ResourceGroupName $RGName -TemplateUri https://raw.githubusercontent.com/MicrosoftLearning/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/main/Instructions/Labs/azuredeploy.json
   ```
  
1. Dans le portail, recherchez et sélectionnez `virtual machines`. Vérifiez que vm1 et vm2 sont **en cours d’exécution**.

### Créer un groupe de sécurité d’application

Des [groupes de sécurité des applications (ASG)](https://learn.microsoft.com/azure/virtual-network/application-security-groups) vous permettent de regrouper des serveurs avec des fonctions similaires. Par exemple, tous les serveurs Web hébergeant votre application. 

1. Dans le portail, recherchez et sélectionnez `Application security groups`.
   
1. Sélectionnez **+Créer** et configurez le groupe de sécurité d’application. 

    | Propriété       | Valeur                        |
    | :------------- | :--------------------------- |
    | Abonnement   | **Sélectionnez votre abonnement** |
    | Resource group | **RG1**                      |
    | Nom           | `app-backend-asg`          |
    | Région         | **USA Est**                  |

1. Sélectionnez **Vérifier + créer**, puis sélectionnez **Créer**.

**Remarque** : vous créez le groupe de sécurité d’application dans la même région que le réseau virtuel existant.

**Associer le groupe de sécurité des applications à l’interface réseau de la machine virtuelle**

1. Dans le portail Azure, recherchez et sélectionnez `VM2`.

1. Dans le panneau **Mise en réseau**, sélectionnez l’onglet **Groupes de sécurité des applications**, puis **Ajouter des groupes de sécurité des applications**.

1. Sélectionnez **app-backend-asg**, puis **Ajouter**.
   
### Créer et associer le groupe de sécurité réseau

Des [groupes de sécurité réseau (NSG)](https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview) sécurisent le trafic réseau dans un réseau virtuel. 

1. Dans le portail, recherchez et sélectionnez `Network security group`.

1. Sélectionnez **+Créer** et configurez le groupe de sécurité réseau. 

    | Propriété       | Valeur                        |
    | :------------- | :--------------------------- |
    | Abonnement   | **Sélectionnez votre abonnement** |
    | Resource group | **RG1**                      |
    | Nom           | `app-vnet-nsg`            |
    | Région         | **USA Est**                  |

1. Sélectionnez **Vérifier + créer**, puis sélectionnez **Créer**.

**Associez le NSG au sous-réseau backend app-vnet.**

Les NSG peuvent être associés à des sous-réseaux et/ou à des interfaces réseau individuelles attachées à des machines Virtuelles Azure. 

1. Sélectionnez **Accéder à la ressource** ou accédez à la ressource **app-vnet-nsg**.

1. Dans le panneau **Paramètres**, sélectionnez **Sous-réseaux**.

1. Sélectionnez **+ Associer**

1. Sélectionnez **app-vnet (RG1)**, puis le sous-réseau **Backend**. Cliquez sur **OK**.

### Créer des règles pour le groupe de sécurité réseau

Un NSG utilise des [règles de sécurité](https://learn.microsoft.com/azure/virtual-network/network-security-group-how-it-works) pour filtrer le trafic réseau entrant et sortant. 

1. Dans la zone de recherche située en haut du portail, entrez **Groupes de sécurité réseau**. Dans les résultats de la recherche, sélectionnez Groupe de sécurité réseau.

1. Sélectionnez **app-vnet-nsg** dans la liste des groupes de sécurité réseau.

1. Dans le panneau **Paramètres**, sélectionnez **Règles de sécurité de trafic entrant**.

1. Sélectionnez **+ Ajouter** et configurez une règle de sécurité de trafic entrant. 

    | Propriété                               | Valeur                          |
    | :------------------------------------- | :----------------------------- |
    | Source                                 | **Any**                        |
    | Plages de ports source                     | **\***                         |
    | Destination                            | **Groupe de sécurité d’application** |
    | Groupe de sécurité d’application de destination | **app-backend-asg**            |
    | Service                                | **SSH**                        |
    | Action                                 | **Autoriser**                      |
    | Priorité                               | **100**                        |
    | Nom                                   | **AllowSSH**                   |


### En savoir plus avec la formation en ligne

+ [Filtrer le trafic réseau avec un groupe de sécurité réseau à l’aide du portail Azure](https://learn.microsoft.com/training/modules/filter-network-traffic-network-security-group-using-azure-portal/). Dans ce module, vous vous concentrez sur le filtrage du trafic réseau à l’aide de groupes de sécurité réseau (NSG) dans le portail Azure. Découvrez comment créer, configurer et appliquer des groupes de sécurité réseau pour améliorer la sécurité réseau.
+ [Sécuriser et isoler l’accès aux ressources Azure en utilisant des groupes de sécurité réseau et des points de terminaison de service](https://learn.microsoft.com/training/modules/secure-and-isolate-with-nsg-and-service-endpoints/). Dans ce module, vous découvrez les groupes de sécurité réseau et comment limiter la connectivité réseau. 

### Points clés

Félicitations ! Vous avez terminé l’exercice. Voici les points clés principaux :

+ Les groupes de sécurité d’application vous permettent d’organiser des machines virtuelles et de définir des stratégies de sécurité réseau en fonction des applications de votre organisation.
+ Un groupe de sécurité réseau Azure est utilisé pour filtrer le trafic réseau entre les ressources Azure dans un réseau virtuel Azure.
+ Vous pouvez associer zéro ou un groupe de sécurité réseau à chaque sous-réseau de réseau virtuel et interface réseau dans une machine virtuelle. 
+ Un groupe de sécurité réseau contient des règles de sécurité qui autorisent ou rejettent le trafic réseau entrant et sortant vers des ressources Azure.
+ Vous regroupez des machines virtuelles dans un groupe de sécurité des applications. Ensuite, vous utilisez le groupe de sécurité d’application comme source ou destination dans les règles de groupe de sécurité réseau.



