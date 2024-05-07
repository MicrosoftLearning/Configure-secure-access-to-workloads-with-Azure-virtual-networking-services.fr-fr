---
lab:
  title: "Exercice\_: contrôler le trafic réseau en direction et en provenance de l’application web"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---

# Labo : contrôler le trafic réseau en direction et en provenance de l’application web

## Scénario

Votre organisation nécessite le contrôle du trafic réseau en direction et en provenance de l’application web. Pour améliorer la sécurité de l’application web, des groupes de sécurité réseau (NSG) et des groupes de sécurité d’application (ASG) peuvent être configurés. Un groupe de sécurité réseau (NSG) est une couche de sécurité qui filtre le trafic réseau en direction et en provenance des ressources Azure, tandis qu’un groupe de sécurité d’application (ASG) permet de gérer collectivement le regroupement de ressources. Ces groupes de sécurité fournissent un contrôle affiné sur le trafic réseau à destination et en provenance des composants d’application web.

### Diagramme de l'architecture

![Diagramme montrant un groupe de sécurité réseau et un groupe de sécurité d’application associés à un réseau virtuel.](../Media/task-2.png)

### Tâches d'apprentissage

- Créez un groupe de sécurité réseau.
- Créez les règles du groupe de sécurité réseau.
- Associez un groupe de sécurité réseau à un sous-réseau.
- Créez et utilisez des groupes de sécurité d’application dans des règles de groupe de sécurité réseau.

## Instructions de l’exercice

### Créer un groupe de sécurité d’application

Un groupe de sécurité d’application vous permet de regrouper des serveurs dont les fonctions sont similaires, comme des serveurs Web.

1. Dans la zone de recherche située en haut du portail, entrez **Groupe de sécurité application**. Dans les résultats de la recherche, sélectionnez Groupes de sécurité d’application.

1. Sélectionnez **+ Créer**.

    Dans l’onglet **De base** de Créer un groupe de sécurité d’application, entrez les informations indiquées dans le tableau ci-dessous :

    | Propriété       | Valeur                        |
    | :------------- | :--------------------------- |
    | Abonnement   | **Sélectionnez votre abonnement** |
    | Resource group | **RG1**                      |
    | Nom           | **app-backend-asg**          |
    | Région         | **USA Est**                  |

1. Sélectionnez **Vérifier + créer**, puis sélectionnez **Créer**.

[En savoir plus sur la création d’un groupe de sécurité d’application](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-application-security-groups).

>**Remarque** : vous créez le groupe de sécurité d’application dans la même région que le réseau virtuel existant.

### Créer et associer le groupe de sécurité réseau

Un groupe de sécurité réseau (NSG) sécurise le trafic réseau dans votre réseau virtuel. Les NSG contiennent une liste de règles de sécurité qui autorisent ou rejettent le trafic réseau vers les ressources connectées aux Réseaux virtuels Azure (VNet). Les NSG peuvent être associés à des sous-réseaux et/ou à des interfaces réseau individuelles attachées à des Machines Virtuelles (VM) Azure.

1. Dans la zone de recherche située en haut du portail, entrez **Groupe de sécurité réseau**. Dans les résultats de la recherche, sélectionnez **Groupe de sécurité réseau**.

1. Sélectionnez **+ Créer**.

    Dans l’onglet **De base** de Créer un groupe de sécurité réseau, entrez les informations indiquées dans le tableau ci-dessous :

    | Propriété       | Valeur                        |
    | :------------- | :--------------------------- |
    | Abonnement   | **Sélectionnez votre abonnement** |
    | Resource group | **RG1**                      |
    | Nom           | **app-vnet-nsg**             |
    | Région         | **USA Est**                  |

    [En savoir plus sur la création d’un groupe de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-a-network-security-group).

1. Sélectionnez **Vérifier + créer**, puis sélectionnez **Créer**.

Dans cette section, vous allez associer le groupe de sécurité réseau au sous-réseau du réseau virtuel que vous avez créé.

1. Dans la zone de recherche située en haut du portail, entrez **Groupe de sécurité réseau**. Dans les résultats de la recherche, sélectionnez Groupe de sécurité réseau.

1. Sélectionnez **app-vnet-nsg** dans la liste des groupes de sécurité réseau.

1. Dans la section Paramètres de **app-vnet-nsg**, sélectionnez **Sous-réseaux**.

1. Dans la page Sous-réseaux, sélectionnez **+ Associer**.

1. Sous **Associer un sous-réseau**, sélectionnez **app-vnet (RG1)** pour Réseau virtuel, et sélectionnez **Serveur principal** pour sous-réseau, puis OK.

    [En savoir plus sur l’association d’un groupe de sécurité réseau à un sous-réseau](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#associate-a-network-security-group-to-a-subnet).

### Créer des règles pour le groupe de sécurité réseau

Un groupe de sécurité réseau (NSG) sécurise le trafic réseau dans votre réseau virtuel.

1. Dans la zone de recherche située en haut du portail, entrez **Groupe de sécurité réseau**. Dans les résultats de la recherche, sélectionnez Groupe de sécurité réseau.

1. Sélectionnez **app-vnet-nsg** dans la liste des groupes de sécurité réseau.

1. Dans la section Paramètres de **app-vnet-nsg**, sélectionnez **Règles de sécurité de trafic entrant**.

1. Sélectionnez **Ajouter**.

1. Sur la page **Ajouter une règle de sécurité de trafic entrant**, entrez les informations du tableau ci-dessous :

    | Propriété                               | Valeur                          |
    | :------------------------------------- | :----------------------------- |
    | Source                                 | **Any**                        |
    | Source port ranges                     | **\***                         |
    | Destination                            | **Groupe de sécurité d’application** |
    | Groupe de sécurité d’application de destination | **app-backend-asg**            |
    | Service                                | **SSH**                        |
    | Action                                 | **Autoriser**                      |
    | Priorité                               | **100**                        |
    | Nom                                   | **AllowSSH**                   |

    [En savoir plus sur la création d’une règle de groupe de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/tutorial-filter-network-traffic#create-a-network-security-group).

### Déployer un modèle ARM à l’aide de Cloud Shell pour créer les machines virtuelles nécessaires à cet exercice

1. Dans le Portail Azure, ouvrez **Azure Cloud Shell** en sélectionnant l’icône située en haut à droite du Portail Azure.

1. Lorsque vous êtes invité à sélectionner **Bash** ou **PowerShell**, sélectionnez **PowerShell**.

    >**Remarque** : si c’est la première fois que vous démarrez **Cloud Shell** et que vous voyez le message **Vous n’avez aucun stockage monté**, sélectionnez l’abonnement que vous utilisez dans ce labo, puis sélectionnez **Créer un stockage**.

1. Déployer le modèle ARM suivant à l’aide de Cloud Shell pour créer les machines virtuelles nécessaires à cet exercice :

>**Remarque** : vous pouvez sélectionner le texte dans la section ci-dessous et le copier/coller dans Cloud Shell.

   ```powershell
   $RGName = "RG1"
   
   New-AzResourceGroupDeployment -ResourceGroupName $RGName -TemplateUri https://raw.githubusercontent.com/MicrosoftLearning/Configure-secure-access-to-workloads-with-Azure-virtual-networking-services/main/Instructions/Labs/azuredeploy.json
   ```
  
1. Pour vérifier que les machines virtuelles **VM1** et **VM2** sont en cours d’exécution, accédez au groupe de ressources **RG1** et sélectionnez **VM1**.

1. Vérifiez que l’état de la machine virtuelle est **En cours d’exécution**.

1. Répétez l’étape précédente pour **VM2**.

### Associer le groupe de sécurité d’application à l’interface réseau de la machine virtuelle

Quand vous avez créé les machines virtuelles, Azure a créé une interface réseau pour chacune d’elles et l’a attachée à celle-ci.

Ajoutez le groupe de sécurité d’application que vous avez créé précédemment à l’interface réseau de VM2.

1. Dans le Portail Azure, accédez au groupe de ressources **RG1** et sélectionnez **VM2**.

1. Accédez à l’onglet Mise en réseau de la machine virtuelle et sélectionnez **+ Ajouter des groupes de sécurité d’application** dans la section **Groupes de sécurité d’application**.

1. Sélectionnez **app-backend-asg** dans la liste des groupes de sécurité d’application.

1. Sélectionnez **Ajouter**.

  [En savoir plus sur l’ajout d’une carte réseau (NIC) à un groupe de sécurité d’application](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-network-interface?tabs=azure-portal#add-or-remove-from-application-security-groups).
