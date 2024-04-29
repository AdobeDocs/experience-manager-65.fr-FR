---
title: Conseils de dépannage pour l’espace de travail AEM Forms
description: Activez les journaux et utilisez le débogueur dans le navigateur pour résoudre les problèmes liés à l’espace de travail AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '738'
ht-degree: 100%

---

# Conseils de dépannage pour l’espace de travail AEM Forms {#troubleshooting-guidelines-for-aem-forms-workspace}

Cet article explique comment déboguer l’espace de travail AEM Forms en activant la journalisation et en utilisant le débogueur dans un navigateur. Il décrit également certains problèmes courants que vous pouvez rencontrer lors de l’utilisation de l’espace de travail AEM Forms et leurs solutions.

## Impossible d’installer le package de l’espace de travail AEM Forms {#unable-to-install-aem-forms-workspace-package}

Une fois que vous avez installé le correctif, ouvrez l’espace de travail AEM Forms. Si vous rencontrez l’erreur « Aucune ressource trouvée », ouvrez le gestionnaire de packages CRX, puis réinstallez le package `adobe-lc-workspace-pkg-<version>.zip`.

Lors de l’installation du package, si vous rencontrez une erreur `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`, procédez comme suit :

1. Connectez-vous à CRXDE Lite. L’URL par défaut est `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Supprimez le nœud suivant :

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Accédez au gestionnaire de packages. L’URL par défaut est `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Recherchez et installez le package `adobe-lc-workspace-pkg-[version].zip`.
1. Redémarrez le serveur d’applications.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

## Journalisation de l’espace de travail AEM Forms {#aem-forms-workspace-nbsp-logging}

Vous pouvez générer des journaux à différents niveaux pour la résolution optimale des erreurs. Prenez l’exemple d’une application complexe. La journalisation au niveau du composant permet de déboguer et de résoudre les problèmes liés à des composants spécifiques.

Dans l’espace de travail AEM Forms :

* Pour obtenir les informations de journalisation sur un fichier de composant spécifique, ajoutez `/log/<ComponentFile>/<LogLevel>` dans l’URL, puis appuyez sur `Enter`. Toutes les informations de journalisation pour le fichier de composant au niveau spécifié de journal sont imprimées sur la console.

* Pour obtenir des informations de journalisation tous les fichiers de composant, ajoutez `/log/all/trace` dans l’URL, puis appuyez sur `Enter`.

* Format du journal : `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>Par défaut, le niveau de journal de tous les composants est défini sur INFO.

* Le niveau de journal défini par l’utilisateur est conservé uniquement pour cette session de navigateur. Lorsque l’utilisateur ou l’utilisatrice actualise la page, le niveau de journal est défini sur sa valeur initiale pour tous les composants.

### Liste des fichiers de composant dans l’espace de travail AEM Forms {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>uisettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>preferencesView</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>taskdetailsView</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### Niveaux de journal disponibles dans l’espace de travail AEM Forms {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATAL
* ERROR
* WARN
* INFO
* DEBUG
* TRACE
* DÉSACTIVÉ

## Informations de débogage pour les navigateurs {#debugging-information-for-browsers}

Les scripts et les styles peuvent être débogués dans différents navigateurs.

* **Débogage dans IE** : pour déboguer l’espace de travail AEM Forms dans IE, voir [https://learn.microsoft.com/fr-fr/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/fr-fr/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **Débogage dans Chrome** : pour ouvrir le débogueur dans Chrome, utilisez le raccourci clavier Ctrl+Maj+I. Pour plus d’informations, consultez le lien [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **Débogage dans Firefox** : plusieurs modules complémentaires sont disponibles pour déboguer des scripts et des styles dans Firefox. Par exemple, Firebug est un utilitaire de débogage de ce type ([https://getfirebug.com](https://getfirebug.com)).

## FAQ {#faqs}

1. Le formulaire PDF n’est pas rendu ou envoyé dans Google Chrome.

   1. Installez le plug-in Adobe® Reader®.
   1. Dans Chrome, ouvrez chrome://plugins pour afficher les plug-ins disponibles.
   1. Désactivez le plug-in PDF Viewer de Chrome et activez le plug-in Adobe Reader.

1. Le formulaire SWF ou le guide n’est pas rendu dans Google Chrome.

   1. Dans Chrome, ouvrez chrome://plugins pour afficher les plug-ins disponibles.
   1. Consultez les détails du plug-in Adobe Flash® Player.
   1. Désactivez PepperFlash sous le plug-in Adobe Flash Player.

1. J’ai personnalisé l’espace de travail AEM Forms, mais je ne parviens pas à voir les modifications.

   Effacez le cache de votre navigateur, puis accédez à l’espace de travail AEM Forms.

1. Que doit faire la personne utilisatrice pour permettre le rendu du formulaire en HTML lors de son ouverture dans le bureau ?

   Sélectionnez le bouton radio HTML du profil par défaut, à l’étape Affecter une tâche, tout en utilisant Workbench.

1. La pièce jointe ne s’affiche pas lorsque vous cliquez dessus.

   Pour afficher les pièces jointes, activez les fenêtres contextuelles dans votre navigateur.

1. Une personne utilisatrice est connectée à une application Forms. Si la personne utilisatrice tente de se connecter à l’espace de travail, il se peut que ce dernier ne se charge pas si la personne utilisatrice ne dispose pas des autorisations d’espace de travail.

   Déconnectez-vous de l’autre application Forms, puis connectez-vous à l’espace de travail.

1. Lors du rendu des formulaires HTML dans l’espace de travail AEM Forms, qui utilisent les propriétés de processus dans leur conception, le bouton Envoyer s’affiche à l’intérieur du formulaire.

   Lorsque vous utilisez les propriétés du processus pendant la conception de formulaires, un bouton Envoyer est ajouté à l’intérieur du formulaire. Lorsqu’il est rendu en tant que fichier PDF dans l’espace de travail AEM Forms, le bouton Envoyer n’est pas visible par la personne utilisatrice finale. Cependant, lors du rendu en tant que formulaire HTML dans l’espace de travail AEM Forms, le bouton Envoyer est visible par la personne utilisatrice finale. Si vous cliquez sur ce bouton Envoyer à l’intérieur du formulaire, rien ne se passe. Cliquez sur le bouton Envoyer au bas de l’espace de travail AEM Forms, en dehors du formulaire, pour terminer la tâche.
