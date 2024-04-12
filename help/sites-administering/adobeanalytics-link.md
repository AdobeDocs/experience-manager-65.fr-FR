---
title: Configurer le suivi des liens Adobe Analytics
description: Découvrez comment configurer le suivi des liens pour SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 9fa3e531-11b3-4b8d-a87c-a08faf06f5b7
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 100%

---


# Configurer le suivi des liens Adobe Analytics{#configuring-link-tracking-for-adobe-analytics}

Lorsque des utilisateurs cliquent sur des liens figurant sur les pages de votre site web, vous pouvez enregistrer diverses informations dans Adobe Analytics. Par exemple, utilisez le suivi des liens pour découvrir comment les utilisateurs et les utilisatrices interagissent avec votre site, ou bien effectuez le suivi des téléchargements de fichiers et des liens de sortie.

## Configuration du suivi des liens pour un framework Adobe Analytics {#configuring-link-tracking-for-an-adobe-analytics-framework}

1. À l’aide de la **Navigation**, accédez via **Déploiement**, **Services Cloud** à la section **Adobe Analytics**.

1. Avec **Afficher les configurations**, ouvrez le framework Adobe Analytics requis.
1. Développez la section **Configuration du suivi des liens** et configurez-la selon vos besoins (cette page fournit des détails supplémentaires) :

   ![Framework Analytics](assets/aa-08.png)

## Suivi des téléchargements de fichiers {#tracking-file-downloads}

Configurez le framework Adobe Analytics de sorte que les fichiers téléchargés à partir des pages associées soient automatiquement suivis en tant que téléchargements dans Adobe Analytics. Lorsque vous activez le suivi des téléchargements, seuls les types de fichiers spécifiés sont suivis.

Le suivi des téléchargements des types de fichiers suivants est effectué par défaut :

* exe
* zip
* wav
* mp3
* mov
* mpg
* avi
* wmv
* doc
* pdf
* xls

Ainsi, avec le suivi des téléchargements activé pour les fichiers PDF, pour chaque clic sur les liens vers des fichiers PDF, le téléchargement du fichier PDF est suivi.

Les propriétés de suivi des téléchargements du framework sont implémentées comme code dans le fichier `analytics.sitecatalyst.js` généré pour une page. L’exemple de code suivant présente la configuration par défaut du suivi des téléchargements :

```
s.trackDownloadLinks= true;
s.linkDownloadFileTypes= 'exe,zip,wav,mp3,mov,mpg,avi,wmv,doc,pdf,xls';
```

Pour permettre le suivi des téléchargements pour votre framework Adobe Analytics :

1. [Ouvrez le framework Adobe Analytics et développez la section Configuration du suivi des liens](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Activez **Suivre les téléchargements**.
1. Dans la zone **Types de fichiers de téléchargement**, saisissez les extensions de nom de fichier pour les types de fichiers dont vous souhaitez effectuer le suivi.

## Suivi des liens externes {#tracking-external-links}

Vous pouvez effectuer le suivi des clics sur des liens externes (liens de sortie) sur vos pages.

Pour effectuer le suivi des liens externes pour votre framework Adobe Analytics :

1. [Ouvrez le framework Adobe Analytics et développez la section **Configuration du suivi des liens**](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configurez les propriétés suivantes en fonction de vos besoins.

Propriétés de suivi lorsque l’utilisateur clique sur des liens externes :

* **Suivi externe**
Active le suivi des liens externes.

* **Filtres externes**
(Facultatif) Définit des filtres pour apparier les URL externes des cibles de lien. Lorsque les liens cibles correspondent au filtre, le lien est suivi. Les filtres externes ne sont utiles que pour effectuer le suivi de certains liens externes sur vos pages.

   Pour spécifier les liens externes à suivre, tapez entièrement ou partiellement l’URL du lien cible. S’il y a plusieurs filtres, séparez-les par une virgule. Entourez les chaînes littérales par des guillemets simples. Si aucune valeur (la valeur par défaut est `''`, deux guillemets simples) n’est entrée, tous les liens externes sont suivis.

* **Filtres internes**
Définit des filtres pour apparier les URL des liens internes. Lorsque le lien cible des URL qui correspondent à ce filtre, le lien n’est pas suivi. La valeur par défaut est une commande JavaScript qui renvoie le nom d’hôte de l’URL pour l’adresse de la fenêtre active.

   Pour spécifier les liens internes qui ne sont pas suivis, tapez entièrement ou partiellement l’URL interne du lien cible. S’il y a plusieurs filtres, séparez-les par une virgule. Entourez les chaînes littérales par des guillemets simples.

  La valeur par défaut est `'javascript:,'+window.location.hostname`.

* **Laisser la chaîne de requête**
Inclut les paramètres URL lors de l’évaluation de correspondances avec des filtres internes et externes.

  Procédez à l’activation pour inclure les paramètres d’URL lors de l’évaluation d’URL du lien cible par rapport aux filtres externes et internes.

Les propriétés de suivi des liens externes sont implémentées en tant que code dans le fichier `analytics.sitecatalyst.js` généré pour une page. L’exemple de code suivant est généré pour une page qui est associée à un framework ayant activé le suivi des liens externes avec la configuration suivante :

* Le filtre externe est `'google.com'`.
* Le filtre interne est la valeur par défaut de `'javascript:,'+window.location.hostname`.
* Les chaînes de requête ne sont pas incluses lors de l’évaluation du lien cible par rapport aux filtres.

```
s.trackExternalLinks= false;
s.linkExternalFilters= 'google.com';
s.linkInternalFilters= 'javascript:,'+window.location.hostname;
s.linkLeaveQueryString= false;
```

## Envoi de données de variable avec les clics sur les liens {#sending-variable-data-with-link-clicks}

Vous pouvez configurer AEM pour envoyer des données d’événement et de variable à Adobe Analytics lorsqu’un utilisateur clique sur un lien. Les propriétés **Configuration du suivi des liens** vous permettent de spécifier les événements et les variables Adobe Analytics à suivre lorsque des clics sur des liens se produisent.

Les mappages de framework déterminent les valeurs d’événement et de variable. Vous pouvez mapper les variables Adobe Analytics sur les variables de vos composants de contenu qui stockent les données que vous souhaitez suivre lorsque l’utilisateur clique sur des liens.

Pour envoyer des données de variable avec des clics sur des liens :

1. [Ouvrez le framework Adobe Analytics et développez la section Configuration du suivi des liens](#configuring-link-tracking-for-an-adobe-analytics-framework).
1. Configurez les propriétés suivantes en fonction de vos besoins.

Pour envoyer des propriétés données variables avec des clics sur des liens :

* **Événements de suivi des liens**
Entrez les variables d’événement Adobe Analytics que vous voulez utiliser pour compter les clics sur les liens.

  S’il y a plusieurs noms de variables, séparez-les par une virgule.

  La valeur par défaut de `None` signifie qu’aucun suivi d’événement n’a lieu.

* **Variables de suivi des liens**
Entrez les variables Adobe Analytics à envoyer à Adobe Analytics lorsque les visiteurs cliquent sur des liens. S’il y a plusieurs noms de variables, séparez-les par une virgule.

  La valeur par défaut de `None` signifie qu’aucune donnée de variable n’est envoyée.

Lorsque vous spécifiez les événements et les variables à envoyer, la configuration est mise en œuvre sous forme de code dans le fichier `analytics.sitecatalyst.js` généré pour une page. L’exemple de code suivant est généré pour une page lorsque le framework suit l’événement `event10` et la propriété `prop4` :

```
s.linkTrackEvents= 'event10';
s.linkTrackVars= 'prop4';
```

## Exemple de configuration du suivi des liens {#example-link-tracking-configuration}

Suivez les procédures ci-dessous pour découvrir le comportement du suivi des liens de l’intégration Adobe Analytics. Les procédures montrent les résultats du [débogueur Adobe Marketing Cloud](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html?lang=fr).

### Configuration générale {#general-configuration}

Cet exemple illustre le fonctionnement du mappage dans le cas du suivi et du débogueur :

1. Ouvrez le framework qui a été associé à une page web.
1. Faites glisser le composant **Page** vers la zone de mappages de la structure. Le composant **Page** fait partie du groupe de composants **Général** dans le Sidekick.

   >[!NOTE]
   >
   >Le composant que vous devez utiliser dans un scénario réel dépend du composant hérité (le cas échéant).
   >
   >Dans le cas contraire, votre propre composant doit y être exposé (en définissant un sous-nœud d’analyse dans son composant de page).

   Configurez le mappage en fonction du tableau suivant, en faisant glisser la variable Analytics (SiteCatalyst) depuis le panneau latéral gauche :

<table>
 <tbody>
  <tr>
   <th>Variable CQ<br /> </th>
   <th>Entrée dans l’explorateur de variables<br /> </th>
   <th>Variable Adobe Analytics</th>
  </tr>
  <tr>
   <td>pagedata.title</td>
   <td>eVar personnalisée 1 (eVar1)</td>
   <td>eVar1</td>
  </tr>
  <tr>
   <td>eventdata.events.pageView</td>
   <td>Personnalisé 1 (event1)</td>
   <td>event1</td>
  </tr>
 </tbody>
</table>

1. Faites glisser le composant Recherche vers la zone de mappages de la structure. Le composant Recherche fait partie du groupe de composants Général dans le sidekick. Configurez le mappage en fonction du tableau suivant, en faisant glisser la variable Analytics (SiteCatalyst) depuis le panneau latéral gauche :

<table>
 <tbody>
  <tr>
   <th>Variable CQ<br /> </th>
   <th>Entrée dans l’explorateur de variables</th>
   <th>Variable Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.keyword</td>
   <td>eVar personnalisée 2 (eVar2)</td>
   <td>eVar2</td>
  </tr>
  <tr>
   <td>eventdata.results</td>
   <td>eVar personnalisée 3 (eVar3)</td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.events.search</td>
   <td>Personnalisé 2 (event2)</td>
   <td>event2</td>
  </tr>
 </tbody>
</table>

### Configurer le suivi externe des liens {#configure-external-link-tracking}

1. Dans votre framework, développez la zone **Configuration du suivi des liens**.
1. Désélectionnez **Suivi des téléchargements**.

1. Sélectionnez **Suivi externe**.
1. Désélectionnez **Laisser la chaîne de requête**.
1. Utilisez la valeur suivante pour que la liste **Filtres externes** l’identifie en tant qu’URL externe :

   `'yahoo.com'`

1. Ajoutez la valeur suivante au champ **Événements de suivi des liens** :

   ```
       event1,event2
   ```

1. Ajoutez la valeur suivante au champ **Variables de suivi des liens** :

   ```
       eVar1,eVar2
   ```

1. Sur la page qui est associée au framework, ajoutez un composant **Texte**. Dans le composant **Texte**, ajoutez un lien hypertexte avec l’adresse suivante :

   `https://search.yahoo.com/?p=this`

1. Passez en **mode Aperçu** et cliquez sur le lien.

L’appel ressemblera à ceci une fois affiché avec Adobe Marketing Cloud Debugger :

![Adobe Marketing Cloud Debugger](assets/aa-leavequerysearch-blank.png)

>[!NOTE]
>
>L’URL ne contient pas la chaîne de requête : `?p=this`

### Inclure le paramètre d’URL {#include-the-url-parameter}

1. Dans le framework, développez la zone **Configuration du suivi des liens**.
1. Activez **Laisser la chaîne de requête**.
1. Chargez à nouveau l’aperçu de la page, puis cliquez sur le lien.

Les détails des appels qui apparaissent dans Adobe Marketing Cloud Debugger sont similaires à l’exemple suivant :

![Adobe Marketing Cloud Debugger (suite)](assets/aa-leavequerysearch-active.png)

>[!NOTE]
>
>Cette fois, l’URL contient la chaîne de requête : `?p=this`

## Suivi des liens ad hoc {#ad-hoc-link-tracking}

Le suivi des liens ad hoc permet aux créateurs de contenu de configurer le suivi des liens pour un composant. La configuration du composant remplace la **configuration du suivi des liens** du framework. Ainsi, sur les pages qui sont associées au framework, les composants **Texte** peuvent être configurés pour le suivi des liens des URL.

Le suivi des liens ad hoc vous permet de suivre les liens de téléchargement et les liens externes, ainsi que les données d’événement et de variable.

Pour activer le suivi des liens ad hoc, vous devez :

* [Associez la page qui contient le composant **Texte** avec le framework](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).
* [Configurez le framework Adobe Analytics pour activer le suivi des liens ad hoc](#enabling-ad-hoc-link-tracking).
* [Configurer le suivi des liens pour un composant Texte](#configuring-link-tracking-for-a-text-component).

### Activation du suivi des liens ad hoc {#enabling-ad-hoc-link-tracking}

Configurez votre framework Adobe Analytics pour activer le suivi des liens ad hoc.

1. Ouvrez le framework Adobe Analytics et développez la section **Configuration du suivi des liens**.

1. Activez le **suivi des liens ad hoc**.

   >[!NOTE]
   >
   >Tous les types d’utilisateurs n’ont pas tous accès à cette case à cocher. Contactez l’administrateur ou l’administratrice de votre site si vous avez besoin d’y accéder.

>[!NOTE]
>
>La configuration XSS Antisamy se trouve à présent dans SLING dans le chemin d’accès **/libs/sling/xss.config.xml** et les règles suivantes doivent être ajoutées pour que les liens ad hoc fonctionnent :

#### Extension de règle de balise d’ancrage {#anchor-tag-rule-extension}

```xml
<attribute name="onclick">
    <literal-list>
        <literal value="CQ_Analytics.Sitecatalyst.customTrack(this)"/>
    </literal-list>
</attribute>
<attribute name="adhocenable">
    <literal-list>
        <literal value="true"/>
        <literal value="false"/>
    </literal-list>
</attribute>
<attribute name="adhocevents">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
<attribute name="adhocevars">
    <regexp-list>
        <regexp name="anything"/>
    </regexp-list>
</attribute>
```

### Configurer le suivi des liens pour un composant texte {#configuring-link-tracking-for-a-text-component}

Pour pouvoir configurer le suivi des liens ad hoc pour les composants **Texte** eux-mêmes, les configurations suivantes doivent avoir déjà été mises en œuvre :

* Le [framework Adobe Analytics est configuré pour permettre le suivi des liens ad hoc](#enabling-ad-hoc-link-tracking).
* La [page qui contient le composant **Texte** est associée au framework](/help/sites-administering/adobeanalytics-connect.md#associating-a-page-with-a-adobe-analytics-framework).

Appliquez la procédure suivante afin de configurer le suivi des liens pour un composant **Texte** :

1. Ouvrez la page en mode d’édition et modifiez le composant **Texte**.

1. Sélectionnez le texte que vous souhaitez utiliser comme hypertexte et cliquez sur le bouton Lien hypertexte.

   ![Icône Lien](do-not-localize/chlimage_1.png)

1. Ajoutez l’URL cible dans la zone Lier à, puis développez la zone Suivi des liens.

   >[!NOTE]
   >
   >Le suivi des liens personnalisés est visible en tant qu’action distincte, en regard de l’action Lier/Dissocier (icône Analytics).
   >
   >Il ne sera activé que lorsque vous aurez sélectionné un lien valide dans le RTE.

   ![Activer le suivi de liens](assets/aa-17.png)

1. Activez le **Suivi des liens personnalisés** pour remplacer la configuration de suivi des liens du framework Adobe Analytics et activer le suivi des liens pour le lien actuel.

1. (Facultatif) Pour suivre les événements avec le clic sur les liens, ajoutez les noms d’événement Adobe Analytics dans le champ **Inclure les variables Adobe Analytics**. Pour ajouter plusieurs noms d’événements, séparez-les par des virgules, par exemple

   `event1, event22`.

1. (Facultatif) Pour suivre les données de variable avec le clic sur les liens, ajoutez les variables Adobe Analytics dans le champ **Inclure les variables Adobe Analytics**. Utilisez l’un des formats suivants :

   * *`<Variable-name>`*: *`<Dynamic Value>`*
   * *`<Variable-name>`*: *`'CONSTANT'`*

   Les exemples suivants illustrent chaque format :

   * `eVar10:pagedata.title`
   * `prop1: 'Aubergine'`

   S’il y a plusieurs valeurs, séparez-les par une virgule.

1. **Cliquez sur OK**.
