---
title: Configurer un compte d’alias de société Dynamic Media
description: Découvrez comment configurer un compte d’alias de société dans Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
exl-id: 2ca7b8b2-573c-40e9-b8c3-f38736e819ef
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 100%

---

<!-- hide: yes
hidefromtoc: yes -->

# À propos de la configuration d’un compte d’alias de société Dynamic Media {#about-dm-alias-acct}

Les URL Dynamic Media et le code incorporé de la visionneuse contiennent le nom du compte de votre société. Ce nom de compte a été créé au moment de la mise en service de Dynamic Media. Il peut y avoir des scénarios où votre entreprise a fait l’objet d’une acquisition ou d’un changement de marque ou où vous souhaitez simplement utiliser un nom plus marquant. Dans ce cas de figure, il n’est pas facile de mettre à jour manuellement le nom de votre compte de société dans toutes les URL et dans le code intégré de la visionneuse prêt à l’emploi. En outre, il est possible que vous impactiez votre référentiel Dynamic Media existant ou que vous impactiez le contenu dynamique. Pour résoudre ce problème, vous pouvez configurer un compte d’alias de société Dynamic Media.

Un compte d’alias de société Dynamic Media permet de s’assurer que toutes les URL Dynamic Media prêtes à l’emploi et le code intégré de la visionneuse dans l’interface utilisateur reflètent toutes les mises à jour apportées à votre contexte d’entreprise, notamment le changement de marque. Un compte d’alias a également un impact positif sur votre optimisation du moteur de recherche (SEO), car les URL Dynamic Media et le code intégré de la visionneuse reflètent le nouveau nom du compte de la société.

Lorsque vous configurez un compte d’alias de société Dynamic Media, tenez compte des points suivants :

* Toute URL Dynamic Media ou tout code incorporé de visionneuse existant sur vos propriétés numériques *dynamiques* doivent être mises à jour manuellement pour prendre en compte le nouveau nom d’alias. Cependant, toutes les URL ou code intégré de visionneuse avec le nom de votre société Dynamic Media d’origine continuent à fonctionner pour les ressources existantes ou nouvelles.
* La fonctionnalité de compte d’alias de société Dynamic Media est limitée au mode de création Experience Manager Assets et à la diffusion. Le nom d’alias de société ne fonctionne pas avec Experience Manager Sites. Les composants WCM (Web Content Management) ne sont pas mis à jour pour cette modification. Ces composants continuent de fonctionner avec le nom de la société Dynamic Media d’origine pour récupérer les ressources Dynamic Media.
* Vous ne pouvez configurer qu’un seul compte d’alias de société sur la page **[!UICONTROL Modifier la configuration de Dynamic Media]**. Cependant, vous pouvez créer autant de comptes d’alias de société par le biais d’un cas d’assistance et refléter manuellement le nom d’alias nécessaire dans les URL Dynamic Media ou le code intégré de la visionneuse.
* La fonctionnalité clé en main [Invalidation du cache](/help/assets/invalidate-cdn-cache-dynamic-media.md) de Dynamic Media invalide les URL avec les comptes de société et d’alias de société configurés dans la page de configuration de Dynamic Media dans les services Cloud.
* Lorsque vous configurez un compte d’alias de société sur la page **[!UICONTROL Modifier la configuration de Dynamic Media]**, pour que l’invalidation du cache réussisse, vous devez invalider simultanément les URL des *deux* comptes **[!UICONTROL Société]** et **[!UICONTROL Alias de la société]**.

Voir également [Créer une configuration Dynamic Media dans les services Cloud](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configurer un compte d’alias de société Dynamic Media {#configure-dm-alias-account}

Vous commencez à configurer un compte d’alias de société Dynamic Media en soumettant d’abord un cas d’assistance. Cette étape est requise.

1. [Utilisez Admin Console pour créer un dossier d’assistance](https://helpx.adobe.com/fr/enterprise/using/support-for-experience-cloud.html).
1. Indiquez les informations suivantes dans votre dossier de support :

   * Nom d’alias de la société Dynamic Media que vous souhaitez utiliser. Le nom doit contenir *exclusivement* des lettres (casse mixte autorisée), chiffres, tirets et traits de soulignement.
   * Votre région.
   * Si des [ensembles de règles](/help/assets/using-rulesets-to-transform-urls.md) ont été utilisés précédemment pour obtenir la diffusion de contenu Dynamic Media par le biais d’un autre nom de compte de société Dynamic Media.

1. Une fois le compte d’alias Dynamic Media créé par l’assistance, dans l’instance d’auteur as a Cloud Service Experience Manager, sélectionnez le logo Experience Manager as a Cloud Service pour accéder à la console de navigation globale.
1. Sur le côté gauche de la console, sélectionnez l’icône Outils, puis **[!UICONTROL Cloud Services > Configuration Dynamic Media]**.
1. Sur la page du navigateur de configuration Dynamic Media, dans le volet de gauche, sélectionnez **[!UICONTROL global]**. Ne sélectionnez pas l’icône de dossier située à gauche de **[!UICONTROL global]**. Sélectionnez ensuite **[!UICONTROL Modifier]**.

   ![Champ de texte Alias de la société Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. À la page **[!UICONTROL Modifier la configuration de Dynamic Media]**, dans le champ de texte **[!UICONTROL Alias de la société]**, saisissez le nom du compte d’alias Dynamic Media que vous avez spécifié précédemment dans votre cas d’assistance.
1. Dans le coin supérieur droit de la page, sélectionnez **[!UICONTROL Enregistrer]**.
Le compte d’alias de la société Dynamic Media est maintenant enregistré et activé ; toutes les URL et le code incorporé de la visionneuse pour les ressources existantes et nouvelles reflètent désormais le nouveau nom d’alias de la société.
