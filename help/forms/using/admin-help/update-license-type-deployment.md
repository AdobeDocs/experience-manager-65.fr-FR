---
title: Mise à jour du type de licence pour le déploiement
description: Mettez à jour le type de licence pour le déploiement à l’aide de la page Changer de licence dans Administration Console.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b975aa1-9270-4098-9af5-c5cc67cb7b5d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 30%

---

# Mise à jour du type de licence pour le déploiement {#update-the-license-type-for-the-deployment}

Lors du processus d’installation d’AEM forms, vous avez utilisé Configuration Manager pour configurer et déployer les modules AEM forms dont vous avez besoin. Par défaut, ces modules sont configurés avec une licence d’évaluation de 60 jours. Utilisez la page Changer de licence dans Administration Console pour modifier le type de licence du déploiement. Les modules actuellement déployés s’affichent sur la page Changer de licence .

La page Changer de licence affiche des informations sur votre licence :

* Type de licence actuel
* Date et heure de la dernière mise à jour de la licence
* Qui a effectué la dernière mise à jour
* État actuel de la licence
* La date à laquelle AEM forms a été installé
* Date d’expiration de la licence actuelle

>[!NOTE]
>
>La modification de licence s’applique à tous les modules déployés. Avant de modifier le type de licence, annulez le déploiement des modules qui ne sont pas sous licence. Ne sélectionnez pas le type de licence Production si la liste des modules déployés contient des modules autres que ceux achetés sur Adobe.

## Mettre à jour le type de licence {#update-the-license-type}

1. Dans Administration Console, cliquez sur Licences.
1. Lisez le contrat de licence de l’utilisateur final d’AEM forms, sélectionnez J’accepte si vous en acceptez les termes, puis cliquez sur Suivant.
1. Sur la page Changer de licence , sélectionnez un type de licence :

   * **EVAL :** Licence d’évaluation de 60 jours
   * **DEV :** licence de développement perpétuelle
   * **NFR :** Licence d’évaluation de 2 ans
   * **IDEV :** abonnement d’un an au programme Adobe Developer
   * **Production :** licence perpétuelle

1. Sélectionnez Oui, le changement de licence est valide pour tous les modules déployés.
1. Cliquez sur Confirmer le changement de licence. Un message vous indique que la licence a été mise à jour avec succès.
