---
demo:
  title: "Démonstration\_: créer et configurer un routage réseau"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---
## Démonstration : créer et configurer un routage réseau

Dans cette démonstration, nous allons découvrir comment créer une table de routage, définir une route personnalisée et associer la route à un sous-réseau. 


**Remarque :**  Cette démonstration nécessite un réseau virtuel avec au moins un sous-réseau.

[Router le trafic réseau - Tutoriel - Portail Azure](https://learn.microsoft.com/azure/virtual-network/tutorial-create-route-table-portal#create-a-route-table)


### Créer une table de route 

1. Quand vous en avez le temps, passez en revue le diagramme du tutoriel. Expliquez pourquoi vous devez créer une route définie par l’utilisateur. 

1. Accédez au portail Azure.

1. Recherchez et sélectionnez **Tables de routage**. Expliquez quand la **propagation des routes de passerelle** doit être utilisée. 

1. Créez une table de routage et expliquez les paramètres inhabituels. 

1. Attendez que la nouvelle table de routage soit déployée.

**Ajouter un itinéraire**

1.  Sélectionnez votre nouvelle table de routage, puis  **Routes**.

1.  Créez une nouvelle **route**. Décrivez les différents **types de tronçons** disponibles. 

1.  Créez la nouvelle route, puis attendez que la ressource soit déployée.
 
### Associer une table de route à un sous-réseau
Une table de routes peut être associée à aucun, à un ou à plusieurs sous-réseaux. Les tables de routage ne sont pas associées à des réseaux virtuels, Vous devez associer une table de routage à chaque sous-réseau auquel vous voulez associer une table de routage.


1.  Accédez au sous-réseau que vous souhaitez associer à la table de routage.

1.  Sélectionnez **Table de routage*, puis choisissez votre nouvelle table de routage. 

1.  **Enregistrez** vos modifications.

 
>**Remarque** : vous pouvez uniquement associer une table de route à des sous-réseaux de réseaux virtuels qui se trouvent au même emplacement et dans le même abonnement Azure que la table de route.

### Tester le pare-feu
À présent, testez le pare-feu pour vérifier que les stratégies de routage et de pare-feu fonctionnent comme prévu. 

1.  Connectez un Bureau à distance à l’adresse IP publique du pare-feu et connectez-vous à la machine virtuelle Srv-Work.
2.  Ouvrez Internet Explorer et accédez à https://www.google.com.
3.  Sélectionnez OK > Fermer sur les alertes de sécurité d’Internet Explorer. La page d’accueil Google doit s’afficher.
4.  Accédez à https://www.microsoft.com. Vous devriez être bloqué par le pare-feu.

Maintenant que vous avez vérifié que les règles de pare-feu fonctionnent :
- Vous pouvez accéder au nom de domaine complet autorisé, mais pas à d’autres.
- Vous pouvez résoudre les noms DNS à l’aide du serveur DNS externe configuré.
 
>**Remarque** : les élèves doivent maintenant être en mesure de terminer le LAB_03




>**Remarque** : les élèves doivent maintenant être en mesure de terminer le LAB_04