---
title: Post-traitement des lettres et communications interactives
description: Le post-traitement des lettres dans Correspondence Management vous permet de créer des post-processus de formulaires et d’AEM, tels que l’impression et le courrier électronique, et de les intégrer dans vos lettres.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
source-git-commit: 6dbec0f41396c2b41d5324c4ecf6f1f33b1d0780
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 73%

---

# Post-traitement des lettres et communications interactives{#post-processing-of-letters-and-interactive-communications}

## Post-traitement {#post-processing}

Les agents peuvent associer et exécuter des workflows de post-traitement sur des lettres et des communications interactives. Le post-traitement à exécuter peut être sélectionné dans la vue Propriétés du modèle de lettre. Vous pouvez configurer des post-traitements pour envoyer par courrier électronique, imprimer, télécopier ou archiver vos lettres finales.

![Post-traitement](assets/ppoverview.png)

Pour associer les post-traitements aux lettres et communications interactives, vous devez commencer par configurer les post-traitements. Deux types de workflows peuvent être exécutés sur les lettres envoyées :

1. **Forms Workflow :** il s’agit des workflows de gestion des processus AEM Forms on JEE. Instructions pour installer [Forms Workflow](#formsworkflow).

1. **AEM Workflow :** les workflows AEM peuvent également être utilisés comme post-traitements pour les lettres envoyées. Instructions pour installer [AEM Workflow](../../forms/using/aem-forms-workflow.md).

## Processus des formulaires {#formsworkflow}

1. Dans AEM, ouvrez Configuration de la console web Adobe Experience Manager pour le serveur à l’aide de l’URL suivante : `https://<server>:<port>/<contextpath>/system/console/configMgr`.

   ![Configuration du gestionnaire](assets/2configmanager-1.png)

1. Sur cette page, recherchez la configuration du SDK de client AEM Forms et développez-la en cliquant dessus.
1. Dans l’URL du serveur, saisissez le nom de votre serveur AEM Forms on JEE, puis cliquez sur **Enregistrer**.

   ![Saisissez le nom du serveur LiveCycle](assets/1cofigmanager.png)

1. Indiquez le nom d’utilisateur et le mot de passe.
1. Assurez-vous que sun.util.calendar est ajouté à la configuration du pare-feu de désérialisation.

   Accédez à la configuration du pare-feu de désérialisation et, dans les classes autorisées des préfixes de package, ajoutez sun.util.calendar.

1. Les serveurs sont désormais mappés et les post-traitements dans AEM Forms on JEE sont disponibles dans l’interface utilisateur AEM lors de la création de lettres.

   ![Création de l’écran des lettres à l’aide des post-traitements répertoriés](assets/0configmanager.png)

1. Pour authentifier un processus/service, copiez le nom d’un processus et retournez sur la page Configurations de la console Web Adobe Experience Manager > Configuration du SDK de client Adobe AEM Forms et ajoutez le processus en tant que nouveau service.

   Par exemple, si la liste déroulante de la page Propriétés affiche le nom du processus comme Forms Workflow -> ValidCCPostProcess/SaveXML, ajoutez un nom de service en tant que `ValidCCPostProcess/SaveXML`.

1. Pour utiliser les processus AEM Forms on JEE pour le post-traitement, configurez les paramètres et les sorties nécessaires. Les valeurs par défaut des paramètres sont indiquées ci-dessous.

   Accédez à la page des configurations de la console web d’Adobe Experience Manager > **[!UICONTROL Configurations de Correspondence Management]** et définissez les paramètres suivants :

   1. **inPDFDoc (paramètre de document PDF) : ** document PDF comme entrée. Cette entrée contient la lettre générée comme entrée. Les noms de paramètre indiqués peuvent être configurés. Ils peuvent être configurés depuis les configurations de Correspondence Management, sous Configuration.
   1. **inXMLDoc (paramètre de données XML) : ** document XML comme entrée. Cette entrée contient des données saisies par l’utilisateur sous la forme XML.
   1. **inXDPDoc (paramètre de document XDP) : ** document XDP comme entrée. Cette entrée contient une disposition sous-jacente (XDP).
   1. **inAttachmentDocs (paramètre de documents joints) : ** paramètre d’entrée de liste. Cette entrée contient toutes les pièces jointes comme entrée.
   1. **redirectURL (sortie d’URL de redirection) : ** type de sortie indiquant l’URL de redirection.

   Votre processus des formulaires doit présenter un paramètre de document PDF ou un paramètre de données XML en tant qu’entrée avec un nom identique à celui spécifié dans les **[!UICONTROL configurations de Correspondence Management]**. Ces informations sont requises pour que le processus soit répertorié dans la liste déroulante Post-traitement.

## Paramètres de l’instance de publication {#settings-on-the-publish-instance}

1. Se connecter à `https://localhost:publishport/aem/forms`.
1. Accédez à **[!UICONTROL Lettres]** pour afficher la lettre publiée disponible sur l’instance de publication.
1. Configurez les paramètres AEM DS. Voir [Configuration des paramètres d’AEM DS](../../forms/using/configuring-the-processing-server-url.md).

>[!NOTE]
>
>Lors de l’utilisation de workflows Forms ou AEM, avant de soumettre un envoi à partir du serveur de publication, il est nécessaire de configurer le service de paramètres DS. Sinon, l’envoi du formulaire échouera.

## Récupération des instances de lettre {#letter-instances-retrieval}

Les instances de lettre enregistrées peuvent être manipulées ultérieurement, comme la récupération des instances de lettre et la suppression des instances de lettre, à l’aide des API suivantes définies dans LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API côté serveur</strong></td>
   <td><strong>Nom de l’opération</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td><p>Public LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Throws ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>Récupérer l’instance de lettre spécifiée </td>
  </tr>
  <tr>
   <td>Public void deleteLetterInstance(String letterInstanceId) throws ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>Supprimer l’instance de lettre spécifiée </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query) throws ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>Cette API récupère les instances de lettre en fonction du paramètre de requête d’entrée. Pour récupérer toutes les instances de lettre, le paramètre de requête doit être transmis comme nul.<br /> </td>
  </tr>
  <tr>
   <td>Public Boolean letterInstanceExists(String letterInstanceName) throws ICCException; </td>
   <td>letterInstanceExists </td>
   <td>Vérifier l’existence d’une instance de lettre par prénom </td>
  </tr>
 </tbody>
</table>

## Association d’un post-traitement à une lettre {#associating-a-post-process-with-a-letter}

Dans l’interface utilisateur CCR, procédez comme suit pour associer un post-traitement à une lettre :

1. Pointez sur une lettre et sélectionnez **Afficher les propriétés**.
1. Sélectionnez **Modifier**.
1. Dans la liste déroulante Propriétés de base , sélectionnez le post-traitement à associer à la lettre dans la liste déroulante Post-traitement. Les post-traitements liés à Forms et à AEM sont répertoriés dans la liste déroulante.
1. Sélectionnez **Enregistrer**.
1. Après avoir configuré la lettre avec le post-traitement, publiez la lettre et, sur l’instance de publication, spécifiez éventuellement l’URL de traitement dans le service Paramètres AEM DS. Cela garantit que le post-traitement est exécuté sur une instance de traitement.

## Rechargement d’une instance de lettre Brouillon  {#reloaddraft}

Une instance de lettre Brouillon peut être rechargée dans l’interface utilisateur à l’aide de l’URL suivante :

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID : identifiant unique de l’instance de lettre envoyée.

Pour plus d’informations sur l’enregistrement d’un brouillon de lettre, voir [Enregistrement de brouillons et envoi d’instances de lettre](../../forms/using/create-correspondence.md#savingdrafts).
