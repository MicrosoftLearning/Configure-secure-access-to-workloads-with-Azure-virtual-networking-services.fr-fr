---
demo:
  title: "Démonstration\_: créer et configurer des réseaux virtuels et le peering"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---
## Démonstration : créer et configurer des réseaux virtuels et le peering


Dans cette démonstration, vous allez créer des réseaux virtuels.

**Remarque :**  vous pouvez utiliser les valeurs suggérées pour les paramètres ou vos propres valeurs personnalisées si vous préférez.

**Remarque :** une **[simulation interactive de laboratoire pour les réseaux virtuels ](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%204?azure-portal=true)** et **[l’appairage de réseaux virtuels](https://mslabs.cloudguides.com/guides/AZ-104%20Exam%20Guide%20-%20Microsoft%20Azure%20Administrator%20Exercise%209?azure-portal=true)** est disponible et vous permet de cliquer sur un labo similaire si vous ne parvenez pas à effectuer une démonstration en direct. Il peut exister de légères différences entre la simulation interactive et la version de démonstration suggérée. Toutefois, les concepts et idées de base présentés sont identiques. 


[Démarrage rapide : créer un réseau virtuel - Portail Azure](https://docs.microsoft.com/azure/virtual-network/quick-create-portal)

### Créer un réseau virtuel dans le portail


   
1.  [Diapositive de prise en charge] Avant de commencer la démonstration, examinons les réseaux virtuels et les concepts clés des Réseaux virtuels Azure. Utilisez cette diapositive pour mettre en évidence les capacités des Réseaux virtuels Azure, ainsi que les concepts et meilleures pratiques relatifs au Réseau virtuel Azure. Lors de la démonstration de la création d’un réseau virtuel, vous pouvez expliquer les concepts de base de l’espace d’adressage, des sous-réseaux, des régions et des abonnements. Vous pouvez également discuter de ces diapositives à la fin et accéder directement à la démonstration.
   
2.  Connectez-vous au portail Azure et recherchez  **Réseaux virtuels**.
   
3.  Créez un réseau virtuel, en expliquant au fur et à mesure les paramètres de base. Veillez à créer au moins un sous-réseau. 
   
4.  Expliquez que le Portail Azure propose une interface conviviale. Les champs obligatoires sont signalés par un astérisque rouge.
   
5.  [Diapositive de prise en charge] Sélectionnez l’onglet Sécurité. Utilisez cette diapositive pour brièvement mettre en évidence les services de sécurité. Ces sujets seront abordés plus en détail dans la suite du cours. En savoir plus sur les services pouvant être déployés dans un réseau virtuel. 
   
6.  [Diapositive de prise en charge] Sélectionnez l’onglet Adresses IP. Utilisez cette diapositive pour examiner la planification des réseaux virtuels et des sous-réseaux. Ajoutez ou modifiez un sous-réseau pour montrer aux élèves comment configurer des sous-réseaux. 
7.  Cliquez Revoir et assurez-vous qu’il n’y a pas d’erreurs de validation.
8.  Cliquez sur Créer, puis attendez que le réseau virtuel soit déployé. Attirez l’attention sur les messages de notification. 
9.  Montrez comment accéder à la ressource.
10. Répétez le processus de création d’un autre réseau virtuel afin de pouvoir présenter VNET Peering.

## Configurer VNET Peering

**Remarque :**  Pour cette démonstration, vous aurez besoin de deux réseaux virtuels.

[Connecter des réseaux virtuels avec le peering VNet - Tutoriel](https://docs.microsoft.com/azure/virtual-network/tutorial-connect-virtual-networks-portal)

**Configurer le peering de réseaux virtuels sur le premier réseau virtuel**

1. Dans le **portail Azure**, sélectionnez le premier réseau virtuel. Examinez la valeur du peering. 

1. Sous **Paramètres**, sélectionnez **Peerings** et **+ Ajoutez** un nouveau peering.

1. Configurez le peering du deuxième réseau virtuel. Utilisez les icônes d’informations pour passer en revue les différents paramètres. 

1. Une fois le peering terminé, passez en revue **l’état du peering**. 

**Confirmer le peering de réseaux virtuels sur le deuxième réseau virtuel**

1. Dans le **portail Azure**, sélectionnez le second réseau virtuel.

1. Sous **Paramètres**, sélectionnez **Peerings**.

1. Notez qu’un appairage a été créé automatiquement. Notez que **l’état du peering** est **Connecté**.


>**Remarque** : les élèves doivent maintenant être en mesure de terminer le LAB_01

