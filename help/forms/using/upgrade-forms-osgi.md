---
title: Mise à niveau vers AEM 6.5 Forms
seo-title: Mise à niveau vers AEM 6.5 Forms
description: Vous pouvez effectuer une mise à niveau directe à partir de AEM 6.1 Forms, AEM 6.2 Forms et LiveCycle ES4 SP1 vers AEM 6.3 Forms.
seo-description: Vous pouvez effectuer une mise à niveau directe à partir de AEM 6.1 Forms, AEM 6.2 Forms et LiveCycle ES4 SP1 vers AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 63%

---


# Mise à niveau vers AEM 6.5 Forms on OSGi {#upgrade-to-aem-forms-osgi}

Vous pouvez effectuer une mise à niveau directe à partir d’AEM 6.3 Forms ou AEM 6.4 Forms vers AEM 6.5 Forms.

Direct upgrade path from **AEM 6.0 Forms, AEM 6.1 Forms**, and **AEM 6.2 Forms** to AEM 6.5 Forms is not available. Perform an intermediate [upgrade to AEM 6.2 Forms](https://helpx.adobe.com/fr/experience-manager/6-2/forms/using/upgrade.html), [upgrade to AEM 6.3 Forms](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/upgrade.html), or [upgrade to AEM 6.4 Forms](/help/forms/using/upgrade.md) and then upgrade from AEM 6.3 Forms, or AEM 6.4 Forms to AEM 6.5 Forms.

Procédez comme suit pour effectuer la mise à niveau d’AEM Forms 6.3 ou AEM Forms 6.4 vers AEM Forms 6.5 :

1. Mettez à niveau l’instance AEM existante vers AEM 6.5. Les étapes sont énumérées ci-dessous :

   1. Installez le dernier Service Pack et les derniers correctifs pour AEM 6.3 Forms ou AEM 6.4 Forms. Pour plus d’informations, reportez-vous à la section Hub [de maintenance d’](https://helpx.adobe.com/fr/experience-manager/aem-releases-updates.html)AEM.
   1. Préparez l’instance source pour la mise à niveau. Pour obtenir des instructions détaillées, reportez-vous à l’article [Mise à niveau vers AEM 6.5](/help/sites-deploying/upgrade.md).
   1. Téléchargez [AEM 6.5 QuickStart](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **(Installations Unix/Linux uniquement)** Si vous utilisez UNIX ou Linux en tant que système d’exploitation sous-jacent, ouvrez la fenêtre de terminal, accédez au dossier contenant crx-quickstart et exécutez la commande suivante :

      `chmod -R 755 ../crx-quickstart`

   1. Upgrade your AEM instance to AEM 6.3. For step by step instructions, see [Upgrading to AEM 6.5](/help/sites-deploying/upgrade.md).

      Avant de passer aux étapes suivantes, attendez que le journal &lt;crx-repository>/error.log contiennent les messages ServiceEvent REGISTERED et ServiceEvent UNREGISTERED.

      >[!NOTE]
      >
      >Une fois le serveur en marche, quelques lots AEM Forms conservent l’état d’installation. Le nombre de lots peut varier d’une installation à l’autre. Vous pouvez ignorer l’état de ces lots en toute sécurité. The bundles are listed at https://&#39;[server]:[port]&#39;/system/console/.

1. Installation du module complémentaire AEM Forms. Les étapes sont énumérées ci-dessous :

   1. Distribution [](https://experience.adobe.com/downloads)de logiciels ouverts. Vous avez besoin d&#39;un Adobe ID pour vous connecter à la distribution de logiciels.
   1. Appuyez sur **[!UICONTROL Adobe Experience Manager]** disponible dans le menu d’en-tête.
   1. In the **[!UICONTROL Filters]** section:
      1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]** .
      1. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option Téléchargements **[!UICONTROL de]** recherche pour filtrer les résultats.
   1. Appuyez sur le nom du pack applicable à votre système d’exploitation, sélectionnez **[!UICONTROL Accepter les termes]** du contrat de licence de l’utilisateur final et appuyez sur **[!UICONTROL Télécharger]**.
   1. Ouvrez [Package Manager](https://docs.adobe.com/content/help/fr-FR/experience-manager-65/administering/contentmanagement/package-manager.html) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
   1. Select the package and click **[!UICONTROL Install]**.

      Vous pouvez également télécharger le package à l’aide du lien direct répertorié dans l’article [AEM Forms Release](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) .

      >[!NOTE]
      >
      >Une fois le package installé, vous êtes invité à redémarrer l’instance AEM. **Ne redémarrez pas immédiatement le serveur.** Avant d’arrêter le serveur AEM Forms, attendez que les messages ServiceEvent REGISTERED et ServiceEvent UNREGISTERED cessent d’apparaître dans le fichier &lt;crx-repository>/error.log et que le journal soit stable. Notez également que quelques packages peuvent rester à l’état installé. Vous pouvez ignorer l’état de ces packages en toute sécurité.

1. Redémarrez l’instance AEM.

1. Procédez aux activités de post-installation.

   * **Exécuter l’utilitaire de migration**

      L’utilitaire de migration rend les formulaires adaptatifs et les actions de gestion de la correspondance des versions antérieures compatibles avec les formulaires AEM 6.5. Vous pouvez télécharger l’utilitaire à partir de la distribution de logiciels AEM. Pour des informations détaillées sur la configuration et l’utilisation de l’utilitaire de migration, voir [l’utilitaire de migration](../../forms/using/migration-utility.md).

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

   * **(Si la mise à niveau d’AEM Forms 6.2 ou des versions antérieures uniquement) Reconfiguration de Adobe Sign**

      Si vous avez configuré Adobe Sign dans la version précédente d’AEM Forms, reconfigurez Adobe Sign à partir des services cloud AEM. Pour plus d’informations, voir [Incorporation d’Adobe Sign à AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Prise en charge de jQuery**

      Dans AEM Forms 6.5, la version de jQuery est mise à jour vers la version 3.2.1 et la version de l’interface utilisateur jQuery est mise à jour vers la version 1.12.1. AEM Form utilise JQuery en **mode non conflictuel** . Ainsi, si vous utilisez une autre version de jQuery, aucun problème ne s’affiche lors de la mise à niveau. Cependant, lorsque vous effectuez une mise à niveau vers AEM Forms 6.5 :

      * Assurez-vous que vos composants personnalisés, le cas échéant, sont compatibles avec les versions jQuery prises en charge.
      * Supprimez les API non prises en charge des composants personnalisés. Voir le guide [de](https://jquery.com/upgrade-guide/3.0/) mise à niveau pour connaître la liste des API supprimées. Par exemple, les API load(), .unload() et .error() sont supprimées. Utilisez la méthode .on() à la place des API mentionnées ci-dessus. Par exemple, remplacez $(&quot;img&quot;).load(fn) par $(&quot;img&quot;).on(&quot;load&quot;, fn).
   * **(Si vous effectuez une mise à niveau à partir d’AEM 6.2 Forms ou de versions précédentes uniquement) Reconfigurez l’analyse et les rapports**

      Dans AEM 6.4 Forms, la variable de trafic pour la source et l’événement de réussite pour l’impression ne sont pas disponibles. Ainsi, lorsque vous effectuez une mise à niveau à partir d’AEM 6.2 Forms ou de versions précédentes, AEM Forms cesse d’envoyer des données au serveur Adobe Analytics et les rapports d’analyse pour les formulaires adaptatifs ne sont pas disponibles. En outre, AEM 6.4 Forms introduit une variable de trafic pour la version de l’analyse de formulaire et de l’événement de réussite pour le temps passé sur un champ. Vous devez donc reconfigurer les analyses et les rapports pour votre environnement AEM Forms. Pour les étapes détaillées, voir [Configuration des analyses et des rapports](../../forms/using/configure-analytics-forms-documents.md).


1. Vérifiez que le serveur a été mis à niveau avec succès, que toutes les données ont également été migrées avec succès, et qu’il peut fonctionner normalement.

   * **Vérifiez l’état des bundles :** assurez-vous que tous les bundles sont actifs.
   * **Vérifiez la réplication et la réplication inversée :** publiez, remplissez et envoyez quelques formulaires migrés. Vérifiez également les données envoyées.
   * **Vérifiez l’accès aux interfaces utilisateur d’administrateur et de développeur :** connectez-vous à une instance d’AEM à partir d’un compte administrateur et vérifiez que vous avez accès aux URL suivantes :

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   Dans AEM 6.4 Forms, la structure du référentiel crx a changé. Si vous effectuez une mise à niveau de 6.3 Forms vers AEM Forms 6.5, utilisez les chemins modifiés pour la personnalisation que vous créez à nouveau. Pour la liste complète des chemins modifiés, voir [Restructuration du référentiel des formulaires dans AEM ](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).

