---
title: Développement d’une application Sandbox
seo-title: Développement d’une application Sandbox
description: Développement d’applications à l’aide de scripts de fondation
seo-description: Développement d’applications à l’aide de scripts de fondation
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Développement d’une application Sandbox {#develop-sandbox-application}

Dans cette section, maintenant que le modèle a été configuré dans la section de l’application [](initial-app.md) initiale et les pages initiales établies dans la section de contenu [](initial-content.md) initial, l’application peut être développée à l’aide de scripts de base, y compris la possibilité d’activer la création avec les composants de communautés. À la fin de cette section, le site Web sera fonctionnel.

## Using Foundation Page Scripts {#using-foundation-page-scripts}

Le script par défaut, créé lorsque le composant qui effectue le rendu du modèle de page de lecture a été ajouté, est modifié pour inclure le fichier head.jsp de la page de base et un fichier body.jsp local.

### Super Ressource Type {#super-resource-type}

La première étape consiste à ajouter une propriété de super-type de ressource au `/apps/an-scf-sandbox/components/playpage` noeud afin qu’il hérite des scripts et des propriétés du super-type.

Utilisation de CRXDE Lite:

<!--Resolve steps below-->
    * Nom : `sling:resourceSuperType`
    * Type : `String`
    * Valeur : &quot;fondation/composants/page&quot;

1. Cliquez sur le vert **[!UICONTROL [+]Ajouter]**
1. Cliquez sur **[!UICONTROL Enregistrer tout]**

![chlimage_1-231](assets/chlimage_1-231.png)

### Scripts de tête et de corps {#head-and-body-scripts}

1. Dans le volet de l’explorateur **CRXDE Lite** , accédez au fichier `/apps/an-scf-sandbox/components/playpage` `playpage.jsp` et cliquez deux fois dessus pour l’ouvrir dans le volet de modification.

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp}

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

1. Conscient des balises de script open/close, remplacez &quot; // TODO ...&quot; avec des scripts pour les parties tête et corps de &lt;html>.

   Avec un super type de `foundation/components/page`, tout script non défini dans ce même dossier sera résolu en un script dans `/apps/foundation/components/page` le dossier (s’il existe), ou en un script dans `/libs/foundation/components/page` le dossier.

#### /apps/an-scf-sandbox/components/playpage/playpage.jsp {#apps-an-scf-sandbox-components-playpage-playpage-jsp-1}

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

1. Le script de base `head.jsp` ne doit pas nécessairement être superposé, mais le script de base `body.jsp` est vide.

   Pour configurer la création, superposez `body.jsp` un script local et insérez un système de paragraphe (parsys) dans le corps :

   1. navigate to `/apps/an-scf-sandbox/components`
   1. sélectionner le `playpage`noeud
   1. cliquez avec le bouton droit et sélectionnez `Create > Create File...`

      * Nom : **body.jsp**
   1. Cliquez sur **[!UICONTROL Enregistrer tout]**
   Ouvrez `/apps/an-scf-sandbox/components/playpage/body.jsp` et collez le texte suivant :

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

1. Cliquez sur **[!UICONTROL Enregistrer tout]**

**Affichez la page dans un navigateur en mode d’édition :**

* Interface utilisateur standard : [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

Vous devriez non seulement voir le titre Lecture **communautaire**, mais aussi l’interface utilisateur pour la modification du contenu de la page.

Le panneau latéral Ressources/Composant s’affiche lorsque les deux panneaux latéraux sont ouverts et que la fenêtre est suffisamment large pour que le contenu latéral et le contenu de la page s’affichent.

![chlimage_1-232](assets/chlimage_1-232.png)

* IU classique : [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

Voici comment la page de lecture apparaît dans l’interface utilisateur classique, y compris avec l’outil de recherche de contenu (cf) :

![chlimage_1-233](assets/chlimage_1-233.png)

## Composants d’AEM Communities {#communities-components}

Pour activer les composants Communities pour la création, suivez d’abord les instructions suivantes :

* [Accès aux composants d’AEM Communities](basics.md#accessing-communities-components)

Pour les besoins de ce sandbox, commencez par les composants **Communautés** suivants (activez-le en cochant la case) :

* Commentaires
* Forum
* Évaluation
* Révisions
* Résumé des révisions (affichage)
* Vote

En outre, sélectionnez des composants **[!UICONTROL généraux]** , tels que

* Image
* Tableau
* Texte
* Titre (Foundation)

>[!NOTE]
>
>Les composants activés pour la page par sont stockés dans le référentiel en tant que valeur de la `components` propriété de la variable
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` .

## Page d’entrée {#landing-page}

Dans un environnement multilingue, la page racine inclurait un script qui analyserait la requête du client pour déterminer la langue souhaitée.

Dans cet exemple simple, la page racine est configurée de manière statique pour rediriger vers la page anglaise, qui peut être développée ultérieurement pour être la page d&#39;entrée principale avec un lien vers la page de lecture.

Remplacez l’URL du navigateur par la page racine : [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* Sélectionner l&#39;icône Informations sur la page
* Sélectionner les propriétés **[!UICONTROL d’ouverture]**
* Sur l’onglet AVANCÉ

   * Pour l’entrée Redirection, accédez à **[!UICONTROL Sites Web > Site de sandbox SCF > Sandbox SCF]**
   * Cliquez sur **[!UICONTROL OK]**

* Cliquez sur **[!UICONTROL OK]**

Une fois le site publié, la navigation vers la page racine d’une instance de publication redirige vers la page anglaise.

La dernière étape avant de jouer avec les composants SCF des communautés est d&#39;ajouter un dossier de bibliothèque client (clientlibs) .... **[⇒](add-clientlibs.md)**