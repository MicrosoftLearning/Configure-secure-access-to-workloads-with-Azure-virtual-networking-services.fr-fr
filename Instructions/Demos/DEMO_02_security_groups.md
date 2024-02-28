---
demo:
  title: "Démonstration\_: créer et configurer des groupes de sécurité réseau"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---
## Démonstration : créer et configurer des groupes de sécurité réseau


Dans cette démonstration, nous allons explorer les groupes de sécurité. 

**Remarque :** une **[simulation interactive de laboratoire pour les réseaux virtuels ](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%2013?azure-portal=true)** est disponible et vous permet de cliquer sur un labo similaire si vous ne parvenez pas à effectuer une démonstration en direct. Il peut exister de légères différences entre la simulation interactive et la version de démonstration suggérée. Toutefois, les concepts et idées de base présentés sont identiques. 

[Restreindre l’accès réseau aux ressources PaaS - Tutoriel - Portail Azure](https://docs.microsoft.com/azure/virtual-network/tutorial-restrict-network-access-to-resources)

### Créer un groupe de sécurité réseau

1. Accédez au portail Azure.

1. Recherchez et sélectionnez  **Groupes de sécurité réseau**.

1. [Diapositive de prise en charge] Créez un NSG en expliquant les paramètres au fur et à mesure. 
 
1. Attendez que le nouveau NSG soit déployé.

**Explorer les règles de trafic entrant et sortant**

1. Sélectionnez votre nouveau NSG.

1. [Diapositive de prise en charge] Expliquez comment le groupe de sécurité réseau peut être associé à des sous-réseaux ou à des interfaces réseau.

1. Expliquez l’objectif des règles de trafic entrant et sortant.  

1. Expliquez les règles de trafic entrant et sortant par défaut. 

1. Créez une nouvelle règle, en expliquant les paramètres au fur et à mesure. Expliquez plus particulièrement la sélection du service (comme HTTPS) et les paramètres de priorité. 
 

### Créer un ASG
 
1. [Diapositive de prise en charge] Recherchez et sélectionnez les  **groupes de sécurité d’application**.

1. Créez un ASG en expliquant les paramètres au fur et à mesure. 
 
1. Attendez que le nouveau ASG soit déployé.

1. Expliquez comment l’ASG peut être associé aux règles de groupe de sécurité réseau.


### Associer les NSG 
1.  Accédez au NSG que vous avez créé
1.  Dans la section Paramètres, sélectionnez Sous-réseaux.
1.  Dans la page Sous-réseaux, sélectionnez + Associer.
1.  Sous Associer un sous-réseau, sélectionnez votre réseau virtuel.


>**Remarque** : les élèves doivent maintenant être en mesure de terminer le LAB_02

