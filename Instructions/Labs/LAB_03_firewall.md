---
lab:
  title: "Exercice\_: protéger l’application web contre le trafic malveillant et bloquer l’accès non autorisé"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---

# Labo : protéger l’application web contre le trafic malveillant et bloquer l’accès non autorisé


## Scénario
Votre organisation souhaite protéger l’application web contre le trafic malveillant et bloquer l’accès non autorisé.

En plus du groupe de sécurité réseau (NSG) et du groupe de sécurité d’application (ASG), vous pouvez configurer un pare-feu pour ajouter une couche de sécurité supplémentaire à l’application web. Un pare-feu protège l’application web contre le trafic malveillant et bloque l’accès non autorisé grâce à des stratégies que vous configurez.

Une stratégie de Pare-feu Azure est une ressource de haut niveau comprenant les paramètres de sécurité et de fonctionnement du Pare-feu Azure. Elle permet de définir une hiérarchie de règles et de garantir la conformité. Dans cette tâche, vous configurez des règles d’application et des règles réseau pour le pare-feu à l’aide de la stratégie de pare-feu. La stratégie du Pare-feu Azure permet de gérer les ensembles de règles que le Pare-feu Azure utilise pour filtrer le trafic. 

### Diagramme de l'architecture

![Diagramme montrant un réseau virtuel avec un pare-feu et une table de routage.](../Media/task-3.png)

### Tâches d'apprentissage
- Créez un Pare-feu Azure.
- Créer et configurer une stratégie de pare-feu
- Créez une collection de règles d’application.
- Créez une collection de règles de réseau.
  
## Instructions de l’exercice

### Créer le sous-réseau Pare-feu Azure dans notre réseau virtuel existant

1. Dans la zone de recherche située en haut du portail, entrez **Réseaux virtuels**. Sélectionnez **Réseaux virtuels** dans les résultats de la recherche.

1. Sélectionnez **app-vnet**.

1. Sélectionner **Sous-réseaux**.

1. Sélectionnez **+ Sous-réseau**.

1. Saisissez les informations suivantes, puis cliquez sur **Enregistrer** :

    | Propriété | Valeur    |
    |:---------|:---------|
    |Nom      | **AzureFirewallSubnet**|
    |Plage d’adresses| **10.1.63.0/24**|

    > **Remarque** : laissez les autres paramètres par défaut.
    

### Créer un pare-feu Azure

1. Dans la zone de recherche située en haut du portail, entrez **Pare-feu**. Sélectionnez **Pare-feu** dans les résultats de la recherche.

1. Sélectionnez **+ Créer**.

1.  Créez un pare-feu à l’aide des valeurs indiquées dans le tableau suivant. Pour toute propriété qui n’est pas spécifiée, utilisez la valeur par défaut.
    >**Remarque** : le déploiement du Pare-feu Azure peut prendre quelques minutes.

    | Propriété | Valeur    |
    |:---------|:---------|
    |Groupe de ressources   | **RG1**  |
    |Nom      | **app-vnet-firewall**|
    |Référence SKU de pare-feu | **Standard**|
    |Gestion de pare-feu | **Utiliser une stratégie de pare-feu pour gérer ce pare-feu**|
    |Stratégie de pare-feu| sélectionnez **Ajouter**| 
    |Nom de stratégie| **fw-policy**|
    |Région| **USA Est**|
    |Niveau de stratégie| **Standard**|
    |Choisir un réseau virtuel | **Utiliser existant**|
    |Réseau virtuel | **app-vnet** (RG1)|
    |Adresse IP publique | Ajouter nouveau : **fwpip**|

    [En savoir plus sur la création d’un pare-feu](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal).

1. Sélectionnez **Vérifier + créer**, puis **Créer**.

### Mettre à jour la stratégie de pare-feu

1. Dans la zone de recherche située en haut du portail, entrez **Stratégie de pare-feu**. Sélectionnez **Stratégies de pare-feu** dans les résultats de la recherche.

1. Sélectionnez **fw-policy**.

1. Sélectionnez **Règles d’application**.

1. Sélectionnez **« + Collection de règles d’application »**.

1. Utilisez les valeurs du tableau suivant. Pour toute propriété qui n’est pas spécifiée, utilisez la valeur par défaut.

    |Propriété|  Valeur |
    |:---------|:---------|
    |Nom   |**app-vnet-fw-rule-collection**|
    |Type de regroupement de règles| **Application**|
    |Priorité|  **200**|
    |Action de regroupement de règles|**Autoriser**|
    |Groupe de regroupement de règles| **DefaultApplicationRuleCollectionGroup**|

    1. Sous **règles**, utilisez les valeurs indiquées dans le tableau suivant.

        |Propriété|  Valeur |
        |:---------|:---------|
        |Nom   |**AllowAzurePipelines**|
        |Type de source|**Adresse IP**|
        |Source|**10.1.0.0/23**|
        |Protocol|**https** |
        |Type de destination|FQDN|
        |Destination|**dev.azure.com, azure.microsoft.com**|

        puis sélectionnez **Ajouter**.

> **Remarque** : la règle **AllowAzurePipelines** permet à l’application web d’accéder à Azure Pipelines. La règle permet à l’application web d’accéder au service Azure DevOps et au site web Azure.

1.  Créez une **collection de règles réseau** qui contient une règle d’adresse IP unique à l’aide des valeurs indiquées dans le tableau suivant. Pour toute propriété qui n’est pas spécifiée, utilisez la valeur par défaut.

1. Sélectionnez **Règles de réseau**.

1. Sélectionnez **« + Collection de règles de réseau »**.

1. Utilisez les valeurs du tableau suivant. Pour toute propriété qui n’est pas spécifiée, utilisez la valeur par défaut.

    |Propriété|  Valeur|
    |:---------|:---------|
    |Nom|  **app-vnet-fw-nrc-dns**|
    |Type de regroupement de règles| **Réseau**|
    |Priorité|  **200**|
    |Action de regroupement de règles|**Autoriser**|
    |Groupe de regroupement de règles| **DefaultNetworkRuleCollectionGroup**|

    1. Sous **règles**, utilisez les valeurs indiquées dans le tableau suivant.

        |Propriété|  Valeur|
        |:---------|:---------|
        |Règle | **AllowDns**|
        |Source|    **10.1.0.0/23**|
        |Protocol|  **UDP**|
        |Ports de destination| **53**|
        |Adresses de destination| **1.1.1.1, 1.0.0.1**|

        Ensuite, sélectionnez **Ajouter**.


    En savoir plus sur la [création d’une règle d’application](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal#configure-an-application-rule) et la [création d’une règle réseau](https://docs.microsoft.com/azure/firewall/tutorial-firewall-deploy-portal#configure-a-network-rule).

1. Pour vérifier que l’état d’approvisionnement des stratégies de pare-feu et de Pare-feu Azure affiche **Réussi**.

1.Dans la zone de recherche située en haut du portail, entrez **Pare-feu**. Sélectionnez **Pare-feu** dans les résultats de la recherche.

1. Sélectionnez **app-vnet-firewall**.

1- Contrôlez que l’**état d’approvisionnement** est **Réussi**.

1- Dans la zone de recherche située en haut du portail, entrez **Stratégies de pare-feu**. Sélectionnez **Stratégies de pare-feu** dans les résultats de la recherche

1. Sélectionnez **fw-policy**.

1- Contrôlez que l’**état d’approvisionnement** est **Réussi**.

