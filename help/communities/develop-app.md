---
title: Développement d’une application Sandbox
description: Découvrez comment développer une application Sandbox qui utilise des scripts de base et inclut la possibilité d’activer la création avec des composants Communities.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 7%

---

# Développement d’une application Sandbox  {#develop-sandbox-application}

Dans cette section, maintenant que le modèle est configuré dans la variable [application initiale](initial-app.md) et les pages initiales établies dans la section [contenu initial](initial-content.md) , vous pouvez développer l’application. Pour ce faire, vous utilisez des scripts de base qui incluent la possibilité d’activer la création avec les composants Communities. À la fin de cette section, vous disposez d’un site web entièrement fonctionnel.

## Utilisation des scripts de page Foundation {#using-foundation-page-scripts}

Le script par défaut, créé lorsque le composant qui effectue le rendu du modèle de page de lecture a été ajouté, est modifié afin d’inclure le fichier head.jsp de la page de base et un fichier body.jsp local.

### Super Resource Type {#super-resource-type}

La première étape consiste à ajouter une propriété de super type de ressource à la propriété `/apps/an-scf-sandbox/components/playpage` afin qu’il hérite des scripts et des propriétés du super type.

Utilisation de CRXDE Lite:

1. Sélectionner un noeud `/apps/an-scf-sandbox/components/playpage`.
1. Dans l’onglet Propriétés , saisissez une nouvelle propriété avec les valeurs suivantes :

   Nom : `sling:resourceSuperType`

   Type : `String`

   Valeur : `foundation/components/page`

1. Cliquez sur le vert **[!UICONTROL +Ajouter]** bouton .
1. Cliquez sur **[!UICONTROL Enregistrer tout]**.

   ![page-script](assets/page-script.png)

### Scripts d’en-tête et de corps {#head-and-body-scripts}

1. Dans **CRXDE Lite** volet d’exploration, accédez à `/apps/an-scf-sandbox/components/playpage` et double-cliquez sur le fichier `playpage.jsp` pour l’ouvrir dans le volet d’édition.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
     An SCF Sandbox Play Component component.
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
    // TODO add your code here
   %>
   ```

1. Conscient des balises de script d’ouverture/de fermeture, remplacez &quot;/ TODO ...&quot; par `includes` des scripts pour les parties head et body de &lt;html>.

   Avec un super type de `foundation/components/page`, tout script non défini dans ce même dossier est résolu sur un script dans `/apps/foundation/components/page` (s’il existe) ou à un script dans `/libs/foundation/components/page` dossier.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: playpage.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <html>
     <cq:include script="head.jsp"/>
     <cq:include script="body.jsp"/>
   </html>
   ```

1. Recouvrement du script de base `head.jsp` n’est pas nécessaire, mais le script de base `body.jsp` est vide.

   Pour configurer la création, superposez `body.jsp` avec un script local et inclure un système de paragraphes (parsys) dans le corps :

   1. Accédez à `/apps/an-scf-sandbox/components`.
   1. Sélectionnez le nœud `playpage`.
   1. Cliquez avec le bouton droit et sélectionnez `Create > Create File...`

      * Nom : **body.jsp**

   1. Cliquez sur **[!UICONTROL Enregistrer tout]**.

   Ouvrir `/apps/an-scf-sandbox/components/playpage/body.jsp` et collez-les dans le texte suivant :

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. Cliquez sur **[!UICONTROL Enregistrer tout]**.

**Affichez la page dans un navigateur en mode d’édition :**

* Interface utilisateur standard: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

Vous ne devriez pas seulement voir l’en-tête **Jeu communautaire**, mais également l’interface utilisateur pour la modification du contenu de la page.

Le panneau latéral Ressources/Composant s’affiche lorsque le panneau latéral est ouvert avec un bouton de basculement et que la fenêtre est suffisamment large pour que le contenu latéral et le contenu de la page s’affichent.

![view-page](assets/view-page.png)

* Interface utilisateur classique : `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

Voici comment la page de lecture s’affiche dans l’IU classique, y compris avec l’outil de recherche de contenu (cf) :

![play-page-view](assets/play-page-view.png)

## Composants Communities {#communities-components}

Pour activer les composants Communities pour la création, commencez par suivre les instructions suivantes :

* [Accès aux composants Communities](basics.md#accessing-communities-components)

Pour les besoins de cet environnement de test, commencez par ces **Communautés** composants (activer en cochant la case) :

* Commentaires
* Forum
* Évaluation
* Révisions
* Résumé des révisions (affichage)
* Votant

En outre, choisissez **[!UICONTROL Général]** les composants, tels que

* Image
* Tableau
* Texte
* Titre (Foundation)

>[!NOTE]
>
>Les composants activés pour la partie page sont stockés dans le référentiel comme valeur de la propriété `components` de la propriété
>
>Nœud `/etc/designs/an-scf-sandbox/jcr:content/playpage/par`.

## Page de destination {#landing-page}

Dans un environnement multilingue, la page racine inclut un script qui analyse la requête du client pour déterminer la langue souhaitée.

Dans cet exemple, la page racine est automatiquement définie pour rediriger vers la page en anglais, qui peut être développée ultérieurement pour être la page d’entrée principale avec un lien vers la page de lecture.

Remplacez l’URL du navigateur par la page racine : `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* Sélectionner l’icône Informations sur la page
* Sélectionner **[!UICONTROL Ouvrir les propriétés]**
* Dans l’onglet AVANCÉ

   * Pour l’entrée de redirection, accédez à **[!UICONTROL Sites web]** > **[!UICONTROL SCF Sandbox Site]** > **[!UICONTROL Environnement de test SCF]**
   * Cliquez sur **[!UICONTROL OK]**

* Cliquez sur **[!UICONTROL OK]**

Une fois le site publié, l’accès à la page racine d’une instance de publication redirige vers la page en anglais.

La dernière étape avant de lire les composants SCF Communities consiste à ajouter un dossier de bibliothèque cliente (clientlibs) .... [Ajout de bibliothèques clientes](add-clientlibs.md)
