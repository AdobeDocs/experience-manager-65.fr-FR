---
title: Mise à jour du type de licence pour le déploiement
description: Mettez à jour le type de licence pour le déploiement à l’aide de la page Changer de licence dans Administration Console.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 100%

---

# Mise à jour du type de licence pour le déploiement {#update-the-license-type-for-the-deployment}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Lors du processus d’installation d’AEM forms, vous avez utilisé Configuration Manager pour configurer et déployer les modules AEM forms dont vous avez besoin. Par défaut, ces modules sont configurés avec une licence d’évaluation de 60 jours. Utilisez la page Changer de licence dans la console d’administration pour modifier le type de licence du déploiement. Les modules actuellement déployés s’affichent sur la page Changer de licence.

La page Changer de licence affiche des informations sur votre licence :

* Type de licence actuel
* Date et heure de la dernière mise à jour de la licence
* Qui a effectué la dernière mise à jour
* Statut actuel de la licence
* Date à laquelle AEM Forms a été installé
* Date d’expiration de la licence actuelle

>[!NOTE]
>
>Le changement de licence s’applique à tous les modules déployés. Avant de modifier le type de licence, annulez le déploiement des modules qui ne sont pas sous licence. Ne sélectionnez pas le type de licence Production si la liste des modules déployés contient des modules autres que ceux acquis auprès d’Adobe.

## Mise à jour du type de licence {#update-the-license-type}

1. Dans la console d’adminitration, cliquez sur Obtention de la licence.
1. Lisez le contrat de licence de l’utilisateur final d’AEM forms, sélectionnez J’accepte si vous en acceptez les termes, puis cliquez sur Suivant.
1. Sur la page Changer de licence , sélectionnez un type de licence :

   * **EVAL :** licence d’évaluation de 60 jours
   * **DEV :** licence de développement perpétuelle
   * **NFR :** licence d’évaluation de 2 ans
   * **IDEV :** abonnement d’un an au programme Adobe Developer
   * **Production :** licence perpétuelle

1. Sélectionnez Oui, le changement de licence est valide pour tous les modules déployés.
1. Cliquez sur Confirmer le changement de licence. Une fois la licence mise à jour, un message vous confirme la réussite de l’opération.
