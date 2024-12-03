---
demo:
  title: "Démonstration\_: créer et configurer un Pare-feu Azure"
  module: Guided Project - Configure secure access to workloads with Azure virtual networking services
---
## Démonstration : créer et configurer un Pare-feu Azure

**Remarque :** le déploiement du Pare-feu Azure peut prendre quelques minutes.

Dans cette démonstration, vous allez explorer le Pare-feu Azure.
Examinez et créez une stratégie de pare-feu et de Pare-feu Azure.
1.  [Diapositive de prise en charge] Avant de commencer la démonstration, penchons-nous sur ce qu’est le Pare-feu Azure.
2.  Accédez au Portail Azure.
3.  Créez un Pare-feu Azure.
4.  (i) sous l’onglet De base, expliquez les options de configuration disponibles à mesure que vous les remplissez. 
5.  Acceptez les autres valeurs par défaut, puis sélectionnez Vérifier + créer.
6.  Une fois le déploiement terminé, accédez à la ressource de pare-feu et examinez la page de vue d’ensemble. 


### Configurer une règle d’application 

1. [Diapositive de prise en charge] Règles de stratégie de Pare-feu Azure

Il s’agit de la règle d’application qui autorise un accès sortant vers www.google.com.
1.  Accédez à la stratégie de pare-feu que vous avez créée.
2.  Sélectionnez Règles d’application.
3.  Sélectionnez Ajouter une collection de règles.
4.  Pour nom, entrez App-Coll01.
5.  Pour Priorité, entrez 200.
6.  Pour Action de collection de règles, sélectionnez Autoriser.
7.  Sous Règles, dans Nom, entrez Allow-Google.
8.  Pour Type de source, sélectionnez Adresse IP.
9.  Pour Source, entrez 10.0.2.0/24.
10. Pour Protocol:port, entrez http, https.
11. Pour Type de destination, sélectionnez FQDN.
12. Pour Destination, entrez www.google.com.
13. Sélectionnez Ajouter.

Le Pare-feu Azure comprend un regroupement de règles intégré pour les noms de domaine complets d’infrastructure qui sont autorisés par défaut. Ces noms de domaine complets sont spécifiques à la plateforme et ne peuvent pas être utilisés à d’autres fins. Pour plus d’informations, consultez Noms de domaine complets d’infrastructure.

### Configurer une règle de réseau
Il s’agit de la règle de réseau qui autorise un accès sortant à deux adresses IP sur le port 53 (DNS).
1.  Sélectionnez Règles de réseau.
2.  Sélectionnez Ajouter une collection de règles.
3.  Pour nom, entrez Net-Coll01.
4.  Pour Priorité, entrez 200.
5.  Pour Action de collection de règles, sélectionnez Autoriser.
6.  Pour Groupe de collection de règles, sélectionnez DefaultNetworkRuleCollectionGroup.
7.  Sous Règles, dans Nom, entrez Allow-DNS.
8.  Pour Type de source, sélectionnez Adresse IP.
9.  Pour Source, entrez 10.0.2.0/24.
10. Pour Protocole, sélectionnez UDP.
11. Pour Ports de destination, entrez 53.
12. Pour Type de destination, sélectionnez Adresse IP.

>**Remarque** : les élèves doivent maintenant être en mesure de terminer le LAB_04
14. Pour Destination, entrez 209.244.0.3, 209.244.0.4.
Il s’agit de serveurs DNS publics gérés par CenturyLink.
15. Sélectionnez Ajouter.

