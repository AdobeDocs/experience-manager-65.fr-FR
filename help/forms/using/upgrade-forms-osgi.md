---
title: Mise à niveau vers AEM 6.5 Forms on OSGi
description: Vous pouvez effectuer une mise à niveau directe à partir d’AEM 6.1 Forms, AEM 6.2 Forms et LiveCycle ES4 SP1 vers AEM 6.3 Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 100%

---

# Mise à niveau vers AEM 6.5 Forms on OSGi {#upgrade-to-aem-forms-osgi}

Vous pouvez effectuer une mise à niveau directe à partir d’AEM 6.3 Forms ou AEM 6.4 Forms vers AEM 6.5 Forms.

Le chemin de mise à niveau direct d’**AEM 6.0 Forms, AEM 6.1 Forms** et **AEM 6.2 Forms** vers AEM 6.5 Forms n’est pas disponible. Effectuez une [mise à niveau intermédiaire vers AEM 6.2 Forms](https://helpx.adobe.com/fr/experience-manager/6-2/forms/using/upgrade.html), [AEM 6.3 Forms](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/upgrade.html) ou [AEM 6.4 Forms](/help/forms/using/upgrade.md), puis effectuez une mise à niveau d’AEM 6.3 Forms ou AEM 6.4 Forms vers AEM 6.5 Forms.

Effectuez les étapes suivantes pour mettre à niveau AEM 6.3 Forms ou AEM 6.4 Forms vers AEM 6.5 Forms :

1. Mettez à niveau l’instance AEM existante vers AEM 6.5. Les étapes sont énumérées ci-dessous :

   1. Installez le dernier Service Pack et les derniers correctifs pour AEM 6.3 Forms ou AEM 6.4 Forms. Pour plus d’informations, voir [AEM Sustenance Hub](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=fr).
   1. Préparez l’instance source pour la mise à niveau. Pour obtenir des instructions détaillées, reportez-vous à l’article [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Téléchargez [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Installations Unix/Linux uniquement)** Si vous utilisez UNIX ou Linux en tant que système d’exploitation sous-jacent, ouvrez la fenêtre de terminal, accédez au dossier contenant crx-quickstart et exécutez la commande suivante :

      `chmod -R 755 ../crx-quickstart`

   1. Mettez à niveau votre instance AEM vers AEM 6.5. Pour obtenir des instructions étape par étape, voir [Mettre à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md).

      Avant de passer aux étapes suivantes, attendez que le journal &lt;crx-repository>/error.log contiennent les messages ServiceEvent REGISTERED et ServiceEvent UNREGISTERED.

      >[!NOTE]
      >
      >Une fois le serveur en marche, quelques lots AEM Forms conservent l’état d’installation. Le nombre de lots peut varier pour chaque installation. Vous pouvez ignorer sans risque l’état de ces lots. Les lots sont répertoriés à l’adresse https://&#39;[serveur]:[port]&#39;/system/console/.

1. Installation du package complémentaire AEM Forms. Suivez les étapes ci-dessous :

   1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
   1. Sélectionnez **[!UICONTROL Adobe Experience Manager]** situé dans le menu d’en-tête.
   1. Dans la section **[!UICONTROL Filtres]** :
      1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]**.
      1. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
   1. Sélectionnez le nom de package applicable à votre système d’exploitation, sélectionnez **[!UICONTROL Accepter les conditions du CLUF]**, puis sélectionnez **[!UICONTROL Télécharger]**.
   1. Ouvrez [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
   1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

      Vous pouvez également télécharger le package via le lien direct répertorié dans l’article [Versions d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).

      >[!NOTE]
      >
      >Une fois le package installé, vous êtes invité à redémarrer l’instance AEM. **N’arrêtez pas le serveur immédiatement.** Avant d’arrêter le serveur AEM Forms, attendez que les messages ServiceEvent REGISTERED et ServiceEvent UNREGISTERED cessent d’apparaître dans le fichier &lt;crx-repository>/error.log et que le journal soit stable. Notez également que quelques packages peuvent rester à l’état installé. Vous pouvez ignorer sans risque l’état de ces packages.

1. Redémarrez l’instance AEM.

   >[!NOTE]
   >
   Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

1. Exécutez les activités postérieures à l’installation.

   * **Exécuter l’utilitaire de migration**

     L’utilitaire de migration rend les formulaires adaptatifs et les actions de gestion de la correspondance des versions antérieures compatibles avec les formulaires AEM 6.5. Vous pouvez télécharger l’utilitaire à partir de la Distribution de logiciels AEM. Pour des informations détaillées sur la configuration et l’utilisation de l’utilitaire de migration, voir [l’utilitaire de migration](../../forms/using/migration-utility.md).

     Si vous utilisez [Exemple pour l’intégration du composant brouillons et envois](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) avec la base de données et que vous mettez à niveau à partir d’une version précédente, exécutez les requêtes SQL suivantes après avoir effectué la mise à niveau :

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(Si vous effectuez une mise à niveau à partir d’AEM 6.2 Forms ou de versions précédentes uniquement) Reconfigurer Adobe Sign**

     Si Adobe Sign était configuré dans la version précédente d’AEM Forms, reconfigurez Adobe Sign à partir des services cloud d’AEM. Pour plus de détails, consultez la section [Intégrer Adobe Sign à AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Prise en charge de jQuery**

     Dans AEM 6.5 Forms, la version de jQuery est mise à jour vers la version 3.2.1 et la version de l’interface utilisateur de jQuery est mise à jour vers la version 1.12.1. AEM Form utilise JQuery en mode **noConflict**. Ainsi, si vous utilisez une autre version de jQuery, aucun problème ne s’affiche lors de l’exécution d’une mise à niveau. Cependant, lorsque vous effectuez une mise à niveau vers AEM 6.5 Forms :

      * Assurez-vous que vos composants personnalisés, le cas échéant, sont compatibles avec les versions jQuery prises en charge.
      * Supprimez les API non prises en charge des composants personnalisés. Voir [guide de mise à niveau](https://jquery.com/upgrade-guide/3.0/) pour la liste des API supprimées. Par exemple, la prise en charge des API load(), .unload() et .error() est supprimée. Utilisez la méthode .on() à la place des API mentionnées ci-dessus. Par exemple, remplacez $(&quot;img&quot;).load(fn) par $(&quot;img&quot;).on(&quot;load&quot;, fn).

   * **(Si vous effectuez une mise à niveau à partir d’AEM 6.2 Forms ou de versions précédentes uniquement) Reconfigurez l’analyse et les rapports**

     Dans AEM Forms 6.4, la variable de trafic pour la source et l’événement de succès de l’impression ne sont pas disponibles. Ainsi, lorsque vous effectuez une mise à niveau à partir d’AEM 6.2 Forms ou de versions précédentes, AEM Forms cesse d’envoyer des données au serveur Adobe Analytics et les rapports d’analyse pour les formulaires adaptatifs ne sont pas disponibles. AEM 6.4 Forms introduit également une variable de trafic pour la version de l’analyse des formulaires et un événement de succès pour le temps passé sur un champ. Dès lors, vous devez reconfigurer les analyses et les rapports de votre environnement AEM Forms. Pour obtenir des instructions détaillées, consultez la section [Configurer les analyses et les rapports](../../forms/using/configure-analytics-forms-documents.md).

1. Vérifiez que le serveur a été mis à niveau avec succès, que toutes les données ont également été migrées avec succès, et qu’il peut fonctionner normalement.

   * **Vérifiez l’état des bundles :** assurez-vous que tous les bundles sont actifs.
   * **Vérifier la réplication et la réplication inverse :** publiez, remplissez et envoyez quelques formulaires migrés. Vérifiez également les données envoyées.
   * **Vérifier l’accès aux interfaces utilisateur d’administration et de développement :** connectez-vous à l’instance AEM à partir d’un compte d’administration et vérifiez que vous avez accès aux URL suivantes :

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   Dans AEM 6.4 Forms, la structure du référentiel crx a changé. Après la mise à niveau d’AEM 6.3 Forms vers AEM 6.5 Forms, utilisez les chemins d’accès modifiés pour la personnalisation que vous créez à nouveau. Pour la liste complète des chemins modifiés, voir [Restructuration du référentiel des formulaires dans AEM](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).
