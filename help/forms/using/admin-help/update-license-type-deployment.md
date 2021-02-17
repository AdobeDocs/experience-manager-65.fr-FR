---
title: Mise à jour du type de licence pour le déploiement
seo-title: Mise à jour du type de licence pour le déploiement
description: Mise à jour du type de licence pour le déploiement à l’aide de la page de modification de licence dans Administration Console.
seo-description: Mise à jour du type de licence pour le déploiement à l’aide de la page de modification de licence dans Administration Console.
uuid: 0152635e-2c00-4944-b9b6-64b368589a91
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e4f31377-ccc9-4986-a3bf-ef2e83d12448
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 100%

---


# Mise à jour du type de licence pour le déploiement {#update-the-license-type-for-the-deployment}

Lors du processus d’installation d&#39;AEM forms, vous avez utilisé Configuration Manager pour configurer et déployer les modules AEM forms dont vous avez besoin. Par défaut, ces modules sont configurés avec une licence d’évaluation de 60 jours. Utilisez la page Changer de licence dans Administration Console pour modifier le type de licence pour le déploiement. Les modules déployés actuellement s’affichent dans la page Changer de licence.

La page Changer de licence contient des informations relatives à la licence :

* le type de licence actuel ;
* la date et l’heure de sa dernière mise à jour ;
* l’auteur de la dernière mise à jour ;
* le statut actuel de la licence ;
* la date à laquelle AEM forms a été installé ;
* la date d’expiration de la licence actuelle.

>[!NOTE]
>
>le changement de licence s’applique à tous les modules déployés. Avant de changer de type de licence, annulez le déploiement de tous les modules ne possédant pas de licence. Ne sélectionnez pas le type de licence Production si la liste des modules déployés contient des modules autres que ceux acquis auprès d’Adobe.

## Mise à jour du type de licence {#update-the-license-type}

1. Dans Administration Console, cliquez sur Obtention de la licence.
1. Lisez le contrat de licence de l’utilisateur final d&#39;AEM forms, sélectionnez J’accepte si vous en acceptez les termes, puis cliquez sur Suivant.
1. Sur la page Changer de licence, sélectionnez un type de licence :

   * **EVAL :** licence d’évaluation de 60 jours
   * **DEV :** licence de développement perpétuelle
   * **NFR :** licence d’évaluation de 2 ans
   * **IDEV :** abonnement d’un an au Programme Développeurs d’Adobe
   * **Production :** licence perpétuelle

1. Sélectionnez Oui, le changement de licence concerne tous les modules déployés.
1. Cliquez sur Confirmer le changement de licence. Une fois la licence mise à jour, un message vous confirme la réussite de l’opération.

