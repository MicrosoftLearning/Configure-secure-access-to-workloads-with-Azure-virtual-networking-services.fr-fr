---
lab:
  title: "Exercice\_: acheminer le trafic vers le pare-feu"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---

# Labo : acheminer le trafic vers le pare-feu

## Scénario

Maintenant qu’un pare-feu est en place avec des stratégies qui appliquent les exigences de sécurité de votre organisation, vous devez acheminer votre trafic réseau vers le sous-réseau du pare-feu afin qu’il puisse filtrer et inspecter le trafic. Les tables de routage permettent de contrôler le routage du trafic réseau à destination et en provenance de l’application web. Le trafic réseau est soumis aux règles du pare-feu lorsque vous acheminez votre trafic réseau vers le pare-feu en tant que sous-réseau de passerelle par défaut.

### Diagramme de l'architecture

![Diagramme montrant un réseau virtuel avec un pare-feu et une table de routage.](../Media/task-3.png)

### Tâches d'apprentissage

- Créez et configurez une table de routage.
- Lier une table de route à un sous-réseau.
  
## Instructions de l’exercice

### Créer une table de routage

1. Enregistrez l’adresse IP privée et publique de **app-vnet-firewall**.

    1. Dans la zone de recherche située en haut du portail, entrez **Pare-feu**. Sélectionnez **Pare-feu** dans les résultats de la recherche.

    1. Sélectionnez **app-vnet-firewall**.

    1. Sélectionnez **Vue d’ensemble**.

        1. Enregistrez l’**adresse IP privée**.

    1. Dans le volet Vue d’ensemble, sélectionnez **fwpip**.

    1. Enregistrez l’**adresse IP publique**.

1. Dans la zone de recherche, entrez **tables de route**. Quand le terme table de route s’affiche dans les résultats de recherche, sélectionnez-le.

1. Dans la page Table de route, sélectionnez **+ Créer**.

1. Dans l’onglet **De base** de Créer une table de route, entrez les informations indiquées dans le tableau ci-dessous :

    | Propriété       | Valeur                        |
    | :------------- | :--------------------------- |
    | Abonnement   | **Sélectionnez votre abonnement** |
    | Resource group | **RG1**                      |
    | Région         | **USA Est**                  |
    | Nom           | **app-vnet-firewall-rt**     |

1. Sélectionnez **Vérifier + créer**, puis sélectionnez **Créer**.

    [En savoir plus sur la création de tables de routage](https://docs.microsoft.com/azure/virtual-network/manage-route-table) et [l’association d’une table de routage à un sous-réseau](https://docs.microsoft.com/azure/virtual-network/tutorial-create-route-table-portal#associate-a-route-table-to-a-subnet).

### Associer la table de route au sous-réseaux

1. Dans la zone de recherche, entrez **tables de route**. Ensuite, sélectionnez Tables de route dans les résultats de la recherche.

1. Sélectionnez **app-vnet-firewall-rt**.

1. Sélectionner **Sous-réseaux**.

1. Sélectionnez **+ Associer**.

1. Sur la page **Associer un sous-réseau**, entrez les informations du tableau ci-dessous :

    | Propriété        | Valeur              |
    | :-------------- | :----------------- |
    | Réseau virtuel | **app-vnet** (RG1) |
    | Sous-réseau          | **frontend**       |

1. Cliquez sur **OK**.

1. Répétez les étapes ci-dessus pour associer la table de route **app-vnet-firewall-rt** au sous-réseau **principal** dans **app-vnet**.

### Créer une route dans la table de route

1. Dans la zone de recherche, entrez **tables de route**. Ensuite, sélectionnez Tables de route dans les résultats de la recherche.

1. Sélectionnez **app-vnet-firewall-rt**.

1. Sélectionnez **Itinéraires**.

1. Sélectionnez **Ajouter**.

1. Sur la page **Ajouter une route**, entrez les informations du tableau ci-dessous :

    | Propriété                            | Valeur                                                   |
    | :---------------------------------- | :------------------------------------------------------ |
    | Nom de l’itinéraire                          | **outbound-firewall**                                   |
    | Type de destination                    | **Adresses IP**                                        |
    | Plage d’adresses IP/CIDR de destination | **0.0.0.0/0**                                           |
    | Type de tronçon suivant                       | **Appliance virtuelle**                                   |
    | adresse de tronçon suivant                    | **adresse IP privée du pare-feu enregistrée précédemment** |

1. Sélectionnez **Ajouter**.

[En savoir plus sur la création de routes](https://docs.microsoft.com/azure/virtual-network/manage-route-table#add-a-route).

À présent, le trafic sortant du serveur frontal et du sous-réseau principal est acheminé vers le pare-feu.
