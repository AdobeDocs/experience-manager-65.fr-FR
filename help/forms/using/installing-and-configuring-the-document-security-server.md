---
title: Installation et configuration du serveur document Security
seo-title: Installation et configuration du serveur document Security
description: 'Utilisez document Security pour distribuer en toute sécurité toutes les informations enregistrées dans un format pris en charge. Seuls les utilisateurs autorisés peuvent accéder aux documents protégés. '
seo-description: 'Utilisez document Security pour distribuer en toute sécurité toutes les informations enregistrées dans un format pris en charge. Seuls les utilisateurs autorisés peuvent accéder aux documents protégés. '
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 42%

---


# Installation et configuration du serveur de sécurité de document {#installing-and-configuring-the-document-security-server}

Utilisez document Security pour distribuer en toute sécurité toutes les informations enregistrées dans un format pris en charge. Seuls les utilisateurs autorisés peuvent accéder aux documents protégés.

La sécurité documentaire d’Adobe Experience Manager Forms garantit que seuls les utilisateurs autorisés peuvent utiliser vos documents. Document Security vous permet de distribuer en toute sécurité toute information enregistrée sous un format pris en charge. Les formats de fichiers pris en charge sont Adobe PDF (Portable Document Format), Microsoft Word, Excel et PowerPoint.

Vous pouvez protéger les documents à l’aide de stratégies. Les paramètres de confidentialité que vous spécifiez dans une stratégie déterminent la mesure dans laquelle un destinataire peut utiliser un document auquel vous appliquez cette stratégie. Par exemple, vous pouvez spécifier si les destinataires sont autorisés à imprimer ou copier du texte, effectuer des modifications ou ajouter des signatures et des commentaires dans des documents protégés.

Les stratégies sont stockées dans Document Security ; vous appliquez les stratégies aux documents par le biais de votre application cliente. Lorsque vous appliquez une stratégie à un document, les paramètres de sécurité spécifiés dans la stratégie protègent les informations que le document contient. Vous pouvez distribuer le document protégé par une stratégie, aux destinataires autorisés par la stratégie.

La sécurité des documents fournit également des clients, des lecteurs et des indexeurs pour protéger les documents, les documents protégés par vue et les documents protégés par index. Pour obtenir des informations détaillées sur la sécurité des documents, voir [à propos de la sécurité des documents](/help/forms/using/admin-help/document-security.md).

## Topologie de déploiement  {#deployment-topology}

La fonctionnalité de sécurité des documents est disponible uniquement dans AEM Forms on JEE. Vous avez besoin d’une instance unique d’AEM Forms on JEE. Vous pouvez également créer une grappe ou une batterie de serveurs AEM Forms, si nécessaire. La topologie suivante est une topologie indicative pour exécuter la fonctionnalité de sécurité des documents. Pour plus d’informations sur la topologie, voir [Topologies d’architecture et de déploiement pour AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

Le diagramme suivant illustre l’architecture standard pour AEM Forms Document Security :

![](do-not-localize/document-security-typical-environment.png)

## Installation de AEM Forms on JEE {#installing-aem-forms-on-jee}

Pour installer et configurer AEM Forms on JEE, procédez comme suit :

1. Téléchargez le programme d’installation d’AEM 6.5 Forms on JEE à partir du site [Adobe Licensing Website (LWS)](https://licensing.adobe.com/). Pour télécharger le programme d’installation, vous devez disposer d’un contrat de Maintenance &amp; Support.
1. Lisez le document [Plateformes prises en charge par AEM Forms on JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) et assurez-vous que les logiciels, le matériel, les systèmes d’exploitation, les serveurs d’applications, les bases de données, les JDK et les autres infrastructures sont prêts à installer AEM Forms on JEE.
1. (Installations non clé en main uniquement) Lisez la section [Préparation à l’installation du serveur unique AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64) ou [Préparation à l’installation du cluster de serveurs AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64) et préparez votre environnement à installer et configurer AEM Forms on JEE.
1. Selon votre environnement et votre serveur d’applications, choisissez l’un des documents suivants et suivez les instructions pour terminer l’installation.

   * [Installation et déploiement d’AEM Forms on JEE à l’aide de JBoss clé en main](https://www.adobe.com/go/learn_aemforms_installTurnkey_64)
   * [Installation et déploiement d’AEM Forms on JEE pour JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64)
   * [Installation et déploiement d’AEM Forms on JEE pour WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64)
   * [Installation et déploiement d’AEM Forms on JEE pour Websphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64)
   * [Configuration d’AEM Forms on JEE sur une grappe JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64)
   * [Configuration d’AEM Forms on JEE sur une grappe WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64)
   * [Configuration d’AEM Forms on JEE sur une grappe WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64)

   >[!NOTE]
   >
   >Dans l’écran de sélection Module du gestionnaire de configuration d’AEM Forms on JEE, sélectionnez l’option Document Security. L&#39;option Sécurité du Document ne nécessite pas la sélection d&#39;un autre module.

## Étapes suivantes {#next-steps}

* [Configuration des options client et serveur](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Création et gestion de stratégies](/help/forms/using/admin-help/creating-policies.md)
* [Création et gestion de jeux de stratégies](/help/forms/using/admin-help/creating-policy-sets.md)
