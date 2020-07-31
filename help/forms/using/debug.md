---
title: Débogage des formulaires HTML5
seo-title: Débogage des formulaires HTML5
description: Ce document présente la marche à suivre pour résoudre divers problèmes bien connus.
seo-description: Ce document présente la marche à suivre pour résoudre divers problèmes bien connus.
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 72%

---


# Débogage des formulaires HTML5 {#debugging-html-forms}

Ce document comprend plusieurs scénarios de résolution des problèmes. Pour chaque scénario, certaines étapes sont fournies pour résoudre le problème. Procédez comme suit et, si le problème persiste, configurez le journal pour obtenir et parcourir les journaux et rechercher les erreurs/avertissements. Pour plus d’informations sur la journalisation des formulaires HTML5, voir [Génération de journaux pour les formulaires HTML5](/help/forms/using/enable-logs.md).

## Problème : lorsque vous effectuez le rendu d’un formulaire, la page d’exception org.apache.sling.api.SlingException s&#39;affiche {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

In the exception details, search for word **caused by**.

Cela est probablement dû au fait qu’un ou plusieurs paramètres de l’URL sont incorrects.

Vérifiez les paramètres suivants :

<table>
 <tbody>
  <tr>
   <td><strong>Paramètre</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>Nom de fichier du modèle</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Chemin d’accès à l’emplacement où le modèle et les ressources connexes résident.</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Chemin d’accès absolu au fichier de données fusionné avec le modèle.<br /> Remarque : Le chemin définit le chemin d’accès absolu au fichier de données.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Octets de données codés au format UTF-8 fusionnés avec le modèle.</td>
  </tr>
 </tbody>
</table>

## Problème : impossible d&#39;effectuer le rendu d&#39;un formulaire (un message d’erreur s’affiche) {#problem-unable-to-render-form}

1. Assurez-vous que les paramètres indiqués sont corrects. Pour plus d’informations sur les paramètres, voir [Paramètres de rendu](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Connectez-vous à CRX Package Manager (à l’adresse https://&lt;serveur>:&lt;port>/crx/packmgr/index.jsp) et vérifiez si les packages suivants sont correctement installés :

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. Connectez-vous à la console Web CQ (console Felix) à l’adresse https://&lt;serveur>:&lt;port>/system/console/bundles.

    Assurez-vous que l’état des bundles suivants est « actif » :

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * Adobe de rendu XFA Forms

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC Connector

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## Problème : le rendu des formulaires ne prend pas les styles en compte {#problem-form-renders-without-styles}

1. In your browser, open **Developer Tools**. Assurez-vous que profil.css est disponible.
1. Si le fichier profil.css n’est pas disponible, connectez-vous à CRX DE à l’adresse https://&lt;serveur>:&lt;port>/crx/de.
1. Dans la hiérarchie de dossiers sur la gauche, accédez à /etc/clientlibs/fd/xfaforms/. Ouvrez les fichiers css.txt répertoriés dans les fichiers.

   * son profil
   * runtime
   * scrollnav
   * toolbar
   * xfalib

1. Vérifiez que les fichiers mentionnés dans le fichier css.txt sont présents dans CRX DE Lite à l’adresse /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Si les fichiers mentionnés ne sont pas disponibles, réinstallez le package adobe-lc-forms-runtime-pkg-&lt;version>.zip.

### Problème : erreur inattendue rencontrée {#problem-unexpected-error-encountered}

1. Dans l’URL du formulaire, ajoutez un paramètre de requête debugClientLibs et définissez sa valeur sur true (par exemple : https://&lt;serveur>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;chemin d’accès>&amp;template=&lt;nom du fichier xdp>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. Dans le navigateur de bureau, comme Chrome, accédez à Outils de développement -> Console.
1. Ouvrez les journaux pour identifier le type d’erreur. Pour plus d’informations sur les journaux, voir [journaux des formulaires HTML5](/help/forms/using/enable-logs.md).
1. Accédez à Outils de développement -> Console. Utilisez la trace de pile pour localiser le code qui déclenche l’erreur. Corrigez l’erreur pour résoudre le problème.

   >[!NOTE]
   >
   >en cas d’échec du script, vérifiez si le même problème se produit également au cours du rendu PDF du formulaire. Si oui, la logique de script du formulaire présente un problème.

## Problème : impossible d’envoyer le formulaire {#problem-unable-to-submit-the-form}

1. Assurez-vous de disposer des droits d’accès au serveur AEM et d’être connecté au serveur.
1. Vérifiez que le paramètre submitUrl est correct.
1. Enable the client side logs as mentioned at [Logs for the HTML5 forms](/help/forms/using/enable-logs.md) using debug option as **1-a5-b5-c5**. Puis lancez le rendu du formulaire et cliquez sur envoyer. Ouvrez la console de dépannage du navigateur et vérifiez s’il se produit une erreur.
1. Recherchez les journaux du serveur comme expliqué dans la section [Journaux des formulaires HTML5](/help/forms/using/enable-logs.md). Vérifiez si une erreur s’est produite dans les journaux du serveur pendant l’envoi.

## Problème : les messages d’erreur localisés ne s’affichent pas {#problem-localized-error-messages-do-not-display}

1. Effectuez le rendu du formulaire avec un paramètre de requête supplémentaire **debugClientLibs=true** dans le navigateur de bureau, puis accédez à Outils de développement -> Ressources et vérifiez le fichier I18N.css.
1. Si le fichier n’est pas disponible, connectez-vous à CRX DE à l’adresse https://&lt;serveur>:&lt;port>/crx/de.
1. Dans la hiérarchie des dossiers sur la gauche, accédez à /libs/fd/xfaforms/clientlibs/I18N et assurez-vous que les fichiers et dossiers suivants existent :

   * Namespace.js
   * LogMessages.js
   * Dossiers de langues

1. Si l’un des fichiers ou dossiers ci-dessus n’existe pas, réinstallez le package **adobe-lc-forms-runtime-pkg-&lt;version>.zip**.
1. Naviguez jusqu’au dossier portant le même nom que le nom du jeu de paramètres régionaux et vérifiez son contenu. Le dossier doit contenir les fichiers suivants :

   * I18N.js
   * js.txt

1. Vérifiez le contenu de js.txt et assurez-vous qu’il possède les entrées suivantes.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problème : l’image ne s’affiche pas {#problem-image-not-showing-up}

1. Assurez-vous que l’URL de l’image est correcte.
1. Vérifiez si votre navigateur prend en charge ce type d’image.
1. In the exception details, search for word **caused by**.

   Cela est probablement dû au fait qu’un ou plusieurs paramètres de l’URL sont incorrects.

   Vérifiez les paramètres suivants :
Texte de l’étape

<table>
 <tbody>
  <tr>
   <td><strong>Paramètre</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>template</td>
   <td>Nom de fichier du modèle</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>Chemin d’accès à l’emplacement où le modèle et les ressources connexes résident.</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Chemin d’accès absolu au fichier de données fusionné avec le modèle.<br /> Remarque : Le chemin définit le chemin d’accès absolu au fichier de données.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Octets de données codés au format UTF-8 fusionnés avec le modèle.</td>
  </tr>
 </tbody>
</table>

1. Dans le navigateur de bureau, accédez à Outils de développement -> Ressources.

   Vérifiez sur le côté gauche, dans Images, que l’image s’affiche.
