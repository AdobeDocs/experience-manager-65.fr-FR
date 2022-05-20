---
title: Installer et configurer le serveur Protection du document
seo-title: Installing and configuring the document security server
description: 'La protection du document vous permet de distribuer en toute sécurité toute information enregistrée dans un format pris en charge. Seuls les utilisateurs autorisés peuvent accéder aux documents protégés. '
seo-description: Use document security to safely distribute any information that you have saved in a supported format. Only authorized users can access protected documents.
uuid: 04c67a84-01ad-45b7-a590-822b1c067d52
contentOwner: khsingh
discoiquuid: 600d13e7-6655-41c5-aab4-c8e9e2a8d14f
role: Admin
exl-id: 4a4bad4a-3e68-43cb-b55c-03b509a5d304
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: ht
source-wordcount: '606'
ht-degree: 100%

---

# Installer et configurer le serveur Protection du document {#installing-and-configuring-the-document-security-server}

La protection du document vous permet de distribuer en toute sécurité toute information enregistrée dans un format pris en charge. Seuls les utilisateurs autorisés peuvent accéder aux documents protégés.

La sécurité documentaire d’Adobe Experience Manager Forms garantit que seuls les utilisateurs autorisés peuvent utiliser vos documents. Document Security vous permet de distribuer en toute sécurité toute information enregistrée sous un format pris en charge. Les formats de fichiers pris en charge sont Adobe PDF (Portable Document Format), Microsoft Word, Excel et PowerPoint.

Vous pouvez protéger les documents à l’aide de stratégies. Les paramètres de confidentialité que vous spécifiez dans une stratégie déterminent la mesure dans laquelle un destinataire peut utiliser un document auquel vous appliquez cette stratégie. Par exemple, vous pouvez spécifier si les destinataires sont autorisés à imprimer ou copier du texte, effectuer des modifications ou ajouter des signatures et des commentaires dans des documents protégés.

Les stratégies sont stockées dans Document Security ; vous appliquez les stratégies aux documents par le biais de votre application cliente. Lorsque vous appliquez une stratégie à un document, les paramètres de sécurité spécifiés dans la stratégie protègent les informations que le document contient. Vous pouvez distribuer le document protégé par une stratégie, aux destinataires autorisés par la stratégie.

La protection du document fournit également des clients, des observateurs et des indexeurs pour protéger les documents, afficher et indexer les documents protégés. Pour plus d’informations sur la protection du document, voir [à propos de la protection du document](/help/forms/using/admin-help/document-security.md).

## Topologie de déploiement  {#deployment-topology}

La fonctionnalité Protection du document est disponible uniquement dans AEM Forms sur JEE. Vous avez besoin d’une seule instance d’AEM Forms sur JEE. Si nécessaire, vous pouvez également créer une grappe ou une ferme de serveurs AEM Forms. La topologie suivante est une topologie indicative pour exécuter la fonctionnalité Protection du document. Pour plus d’informations sur la topologie, voir [Topologies d’architecture et de déploiement pour AEM Forms](aem-forms-architecture-deployment.md).

<!--fix above link-->

![](do-not-localize/document-security-server_topology.png)

Le diagramme suivant illustre l’architecture standard pour AEM Forms Document Security :

![](do-not-localize/document-security-typical-environment.png)

## Installation d’AEM Forms on JEE {#installing-aem-forms-on-jee}

Pour installer et configurer AEM Forms sur JEE, procédez comme suit :

1. Téléchargez le programme d’installation d’AEM 6.5 Forms on JEE à partir du site [Adobe Licensing Website (LWS)](https://licensing.adobe.com/). Pour télécharger le programme d’installation, vous devez disposer d’un contrat de Maintenance &amp; Support.
1. Lisez le [Document sur les plateformes prises en charge par AEM Forms sur JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) et assurez-vous que les logiciels, le matériel, les systèmes d’exploitation, le serveur d’applications, les bases de données, les JDK et toute autre infrastructure soient prêts à installer AEM Forms sur JEE.
1. (Installations non clé en main uniquement) Lisez la section [Préparer à l’installation d’AEM Forms sur un seul serveur](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64_fr) ou [Préparer à l’installation de la grappe de serveurs AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareInstallcluster_64_fr) et préparez votre environnement pour installer et configurer AEM Forms sur JEE.
1. En fonction de votre environnement et de votre serveur d’application, sélectionnez l’un des documents suivants et suivez les instructions pour terminer l’installation

   * [Installation et déploiement d’AEM Forms on JEE à l’aide de JBoss clé en main](https://www.adobe.com/go/learn_aemforms_installTurnkey_64_fr)
   * [Installation et déploiement d’AEM Forms on JEE pour JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_64_fr)
   * [Installation et déploiement d’AEM Forms on JEE pour WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_64_fr)
   * [Installation et déploiement d’AEM Forms on JEE pour Websphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_64_fr)
   * [Configuration d’AEM Forms on JEE sur une grappe JBoss](https://www.adobe.com/go/learn_aemforms_clusterJBoss_64_fr)
   * [Configuration d’AEM Forms on JEE sur une grappe WebLogic](https://www.adobe.com/go/learn_aemforms_clusterWebLogic_64_fr)
   * [Configuration d’AEM Forms on JEE sur une grappe WebSphere](https://www.adobe.com/go/learn_aemforms_clusterWebSphere_64_fr)

   >[!NOTE]
   >
   >Dans l’écran de sélection des modules du gestionnaire de configuration d’AEM Forms sur JEE, sélectionnez l’option Protection du document. L’option Protection du document ne nécessite la sélection d’aucun autre module.

## Étapes suivantes {#next-steps}

* [Configurer les options du client et du serveur](/help/forms/using/admin-help/configuring-client-server-options.md)
* [Créer et gérer des stratégies](/help/forms/using/admin-help/creating-policies.md)
* [Créer et gérer des jeux de stratégies](/help/forms/using/admin-help/creating-policy-sets.md)
