---
title: Configuration d’un compte d’alias de société Dynamic Media
description: Découvrez comment configurer un compte d’alias d’entreprise dans Dynamic Media.
contentOwner: Rick Brough
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User,Admin
mini-toc-levels: 4
hide: true
hidefromtoc: true
source-git-commit: 2706a069bea731da1f84c15e2da02b53a9db4d28
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 9%

---

# A propos de la configuration d’un compte d’alias d’entreprise Dynamic Media {#about-dm-alias-acct}

Les URL Dynamic Media et le code incorporé de la visionneuse contiennent le nom du compte de votre société. Ce nom de compte a été créé au moment de la mise en service de Dynamic Media. Il peut y avoir des scénarios où votre entreprise a fait l’objet d’une acquisition ou d’un changement de marque ou où vous souhaitez simplement utiliser un nom plus mémorable. Dans ce cas de figure, il n’est pas facile de mettre à jour manuellement le nom de votre compte d’entreprise dans toutes les URL et le code intégré de la visionneuse prêts à l’emploi. En outre, il est possible que vous impactiez votre référentiel Dynamic Media existant ou que vous impactiez le contenu en direct. Pour résoudre ce problème, vous pouvez configurer un compte d’alias de société Dynamic Media.

Un compte d’alias d’entreprise Dynamic Media permet de s’assurer que toutes les URL Dynamic Media prêtes à l’emploi et le code intégré de la visionneuse dans l’interface utilisateur reflètent toutes les mises à jour apportées à votre contexte d’entreprise, telles que le changement de marque. Un compte d’alias a également un impact positif sur votre optimisation du moteur de recherche (SEO), car les URL Dynamic Media et le code intégré de la visionneuse reflètent le nouveau nom du compte de la société.

Lorsque vous configurez un compte d’alias de société Dynamic Media, tenez compte des points suivants :

* Toute URL Dynamic Media ou tout code incorporé de visionneuse existant sur votre *live* les propriétés numériques doivent être mises à jour manuellement pour prendre en compte le nouveau nom d’alias. Cependant, tout code incorporé d’URL ou de visionneuses avec le nom de votre société Dynamic Media d’origine continue à fonctionner pour les ressources existantes ou nouvelles.
* La fonctionnalité de compte d’alias d’entreprise Dynamic Media est limitée au mode et à la diffusion de création Experience Manager Assets. Le nom d’alias de l’entreprise ne fonctionne pas avec Experience Manager Sites. Les composants WCM (Web Content Management) ne sont pas mis à jour pour cette modification. Ces composants continuent de fonctionner avec le nom de la société Dynamic Media d’origine pour récupérer les ressources Dynamic Media.
* Vous ne pouvez configurer qu’un seul compte d’alias de société sur l’événement **[!UICONTROL Modifier la configuration de Dynamic Media]** page. Cependant, vous pouvez créer autant de comptes d’alias d’entreprise par le biais d’un cas d’assistance et refléter manuellement le nom d’alias nécessaire dans les URL Dynamic Media ou le code intégré de la visionneuse.
* La clé en main [Invalidation du cache](/help/assets/invalidate-cdn-cache-dynamic-media.md) La fonctionnalité de Dynamic Media invalide les URL avec les comptes d’alias d’entreprise et d’entreprise configurés dans la page de configuration de Dynamic Media en Cloud Services.
* Lorsque vous configurez un compte d’alias d’entreprise sur le **[!UICONTROL Modifier la configuration de Dynamic Media]** , pour que l’invalidation du cache réussisse, vous devez invalider les URL pour *both* la valeur **[!UICONTROL Société]** et la variable **[!UICONTROL Alias de la société]** compte, simultanément.

Voir aussi [Création d’une configuration Dynamic Media dans les Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)

## Configuration d’un compte d’alias de société Dynamic Media {#configure-dm-alias-account}

Vous commencez à configurer un compte d’alias de société Dynamic Media en soumettant d’abord un cas d’assistance. Cette étape est requise.

1. [Utilisez Admin Console pour créer un dossier d’assistance](https://helpx.adobe.com/fr/enterprise/using/support-for-experience-cloud.html).
1. Indiquez les informations suivantes dans votre dossier de support :

   * Nom d’alias de la société Dynamic Media que vous souhaitez utiliser. Le nom doit contenir *only* lettres (casse mixte autorisée), chiffres, tirets et traits de soulignement.
   * Votre région.
   * Si [ensembles de règles](/help/assets/using-rulesets-to-transform-urls.md) sont utilisées précédemment pour obtenir la diffusion de contenu Dynamic Media par le biais d’un autre nom de compte de société Dynamic Media.

1. Une fois le compte d’alias Dynamic Media créé par l’assistance, dans l’instance d’auteur as a Cloud Service Experience Manager, sélectionnez le logo as a Cloud Service du Experience Manager pour accéder à la console de navigation globale.
1. Sur le côté gauche de la console, sélectionnez l’icône Outils, puis **[!UICONTROL Cloud Services > Configuration Dynamic Media]**.
1. Sur la page du navigateur de configuration Dynamic Media, dans le volet de gauche, sélectionnez **[!UICONTROL global]**. Ne sélectionnez pas l’icône de dossier située à gauche de **[!UICONTROL global]**. Sélectionnez ensuite **[!UICONTROL Modifier]**.

   ![Champ de texte Alias de la société Dynamic Media](/help/assets/assets-dm/dm-company-alias.png)

1. Sur le **[!UICONTROL Modifier la configuration de Dynamic Media]** , dans la **[!UICONTROL Alias de la société]** champ de texte, saisissez le nom du compte d’alias Dynamic Media que vous avez spécifié précédemment dans votre cas de support.
1. Dans le coin supérieur droit de la page, sélectionnez **[!UICONTROL Enregistrer]**.
Le compte d’alias de la société Dynamic Media est maintenant enregistré et activé ; toutes les URL et le code incorporé de la visionneuse pour les ressources existantes et nouvelles reflètent désormais le nouveau nom d’alias de la société.