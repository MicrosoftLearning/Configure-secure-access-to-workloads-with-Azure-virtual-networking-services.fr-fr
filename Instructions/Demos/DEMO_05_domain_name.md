---
demo:
  title: "Démonstration\_: créer et configurer Azure DNS"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---
## Démonstration : créer et configurer Azure DNS

Dans cette démonstration, vous allez explorer Azure DNS.

[Tutoriel : héberger votre domaine et votre sous-domaine - Azure DNS](https://docs.microsoft.com/azure/dns/dns-delegate-domain-azure-dns)


**Créer une zone DNS privée**

1. Accédez au portail Azure.

1. Recherchez le service **Zones DNS**.

1. Créez une **zone DNS** et expliquez l’objectif de la zone. Pour le nom, vous pouvez utiliser contoso.internal.com.

1.  Attendez que la zone DNS soit créée. Il peut être nécessaire  **d’actualiser** la page.

**Ajouter un jeu d’enregistrements DNS**


[Tutoriel : créer un enregistrement d’alias pour référencer un enregistrement de ressource de zone](https://learn.microsoft.com/azure/dns/tutorial-alias-rr)

1. Une fois votre zone créée, sélectionnez **+Jeu d’enregistrements**.

1. Utilisez la liste déroulante **Type** pour voir les différents types d’enregistrements. Expliquez comment les différents types d’enregistrements sont utilisés. Notez que les informations de l’enregistrement changent à mesure que vous sélectionnez différents types d’enregistrements.

1. Créez un enregistrement **A** à titre d’exemple. 

**Lier VNet pour l’inscription automatique**

1.  Une fois la zone DNS déployée, examinez la page de vue d’ensemble avec les élèves.
1.  Liez la zone DNS privée à un réseau virtuel en créant une liaison de réseau virtuel.
1.  Dans le volet gauche, sélectionnez Liens de réseau virtuel.
1.  Sélectionnez Ajouter.
1.  Pour nom du lien, entrez myLink.
1.  Pour Réseau virtuel, sélectionnez myAzureVNet.
1.  Activez la case à cocher Activer l’inscription automatique.
1.  Cliquez sur OK.

>**Remarque** : les élèves doivent maintenant être en mesure de terminer le LAB_05