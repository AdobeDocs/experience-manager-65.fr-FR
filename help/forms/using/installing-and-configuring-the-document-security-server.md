---
title: Installation et configuration du serveur Document Security
seo-title: Installation et configuration du serveur Document Security
description: 'Utilisez Document Security pour distribuer en toute sécurité les informations enregistrées dans un format pris en charge. Seuls les utilisateurs autorisés peuvent accéder aux documents protégés. '
seo-description: 'Utilisez Document Security pour distribuer en toute sécurité les informations enregistrées dans un format pris en charge. Seuls les utilisateurs autorisés peuvent accéder aux documents protégés. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Installation et configuration du serveur Document Security {#installing-and-configuring-the-document-security-server}

Utilisez Document Security pour distribuer en toute sécurité les informations enregistrées dans un format pris en charge. Seuls les utilisateurs autorisés peuvent accéder aux documents protégés.

La sécurité documentaire d’Adobe Experience Manager Forms garantit que seuls les utilisateurs autorisés peuvent utiliser vos documents. Document Security vous permet de distribuer en toute sécurité toute information enregistrée sous un format pris en charge. Les formats de fichiers pris en charge sont Adobe PDF (Portable Document Format), Microsoft Word, Excel et PowerPoint.

Vous pouvez protéger les documents à l’aide de stratégies. Les paramètres de confidentialité que vous spécifiez dans une stratégie déterminent la mesure dans laquelle un destinataire peut utiliser un document auquel vous appliquez cette stratégie. Par exemple, vous pouvez spécifier si les destinataires sont autorisés à imprimer ou copier du texte, effectuer des modifications ou ajouter des signatures et des commentaires dans des documents protégés.

Les stratégies sont stockées dans Document Security ; vous appliquez les stratégies aux documents par le biais de votre application cliente. Lorsque vous appliquez une stratégie à un document, les paramètres de sécurité spécifiés dans la stratégie protègent les informations que le document contient. Vous pouvez distribuer le document protégé par une stratégie, aux destinataires autorisés par la stratégie.

Document Security fournit également des clients, des lecteurs et des indexeurs pour protéger des documents, afficher des documents protégés et indexer des documents protégés. Pour plus d’informations sur Document Security, voir [A propos de Document Security](/help/forms/using/admin-help/document-security.md).

## Topologie de déploiement  {#deployment-topology}

La fonctionnalité Document Security est disponible uniquement dans AEM Forms sur JEE. Vous avez besoin d’une instance unique d’AEM Forms sur JEE. Vous pouvez également créer une grappe ou une batterie de serveurs AEM Forms, si nécessaire. La topologie suivante est une topologie indicative pour exécuter la fonctionnalité Document Security. Pour plus d’informations sur la topologie, voir [Topologies d’architecture et de déploiement pour AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

Le diagramme suivant illustre l’architecture standard pour AEM Forms Document Security :

![](do-not-localize/document-security-typical-environment.png)

## Installation d’AEM Forms sur JEE {#installing-aem-forms-on-jee}

Effectuez les étapes suivantes pour installer et configurer AEM Forms sur JEE :

1. Téléchargez le programme d’installation d’AEM 6.5 Forms on JEE à partir du site [Adobe Licensing Website (LWS)](https://licensing.adobe.com/). Pour télécharger le programme d’installation, vous devez disposer d’un contrat de Maintenance &amp; Support.
1. Lisez le document [Plateformes prises en charge par](/help/forms/using/aem-forms-jee-supported-platforms.md) AEM Forms sur JEE et assurez-vous que les logiciels, le matériel, les systèmes d’exploitation, le serveur d’applications, les bases de données, les JDK et d’autres infrastructures sont prêts à installer AEM Forms sur JEE.
1. (Installations non clé en main uniquement) Lisez la section [Préparation à l’installation du serveur](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) unique AEM Forms ou [Préparation à l’installation de la grappe](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) de serveurs AEM Forms et préparez votre environnement pour installer et configurer AEM Forms sur JEE.
1. Selon votre environnement et votre serveur d’applications, sélectionnez l’un des documents suivants et suivez les instructions pour terminer l’installation.

   * [Installation et déploiement d’AEM Forms on JEE à l’aide de JBoss clé en main](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Installation et déploiement d’AEM Forms on JEE pour JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Installation et déploiement d’AEM Forms on JEE pour WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Installation et déploiement d’AEM Forms on JEE pour Websphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configuration d’AEM Forms on JEE sur une grappe JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configuration d’AEM Forms on JEE sur une grappe WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configuration d’AEM Forms on JEE sur une grappe WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)
   >[!NOTE]
   >
   >Dans l’écran de sélection de module du gestionnaire de configuration d’AEM Forms sur JEE, sélectionnez l’option Document Security. L’option Document Security ne nécessite pas la sélection d’un autre module.

## Étapes suivantes {#next-steps}

* [Configuration des options client et serveur](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Création et gestion des stratégies](/help/forms/using/admin-help/creating-policies.md)
* [Création et gestion des jeux de stratégies](/help/forms/using/admin-help/creating-policy-sets.md)
