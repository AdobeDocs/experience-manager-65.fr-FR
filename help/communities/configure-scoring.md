---
title: Scores et insignes essentiels
seo-title: Scores et insignes essentiels
description: Présentation de la fonction Notation et Badges
seo-description: Présentation de la fonction Notation et Badges
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 1%

---


# Scores et insignes essentiels {#scoring-and-badges-essentials}

La fonction de notation et de badges AEM Communities permet d&#39;identifier et de récompenser les membres de la communauté.

Les détails de la configuration de la fonction sont décrits dans la section

* [Score et badges des communautés](/help/communities/implementing-scoring.md)

Cette page contient des détails techniques supplémentaires :

* Comment [afficher un badge](#displaying-badges) sous forme d’image ou de texte
* Comment activer la journalisation étendue du [débogage](#debug-log-for-scoring-and-badging)
* Comment [accéder à l&#39;UGC](#ugc-for-scoring-and-badging) en rapport avec la notation et l&#39;insu

>[!CAUTION]
>
>La structure de mise en oeuvre visible dans le CRXDE Lite peut être modifiée.

## Affichage de badges {#displaying-badges}

Si un badge s&#39;affiche sous forme de texte ou d&#39;image est contrôlé côté client dans le modèle HBS.

Par exemple, recherchez `this.isAssigned` dans `/libs/social/forum/components/hbs/topic/list-item.hbs`:

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

Si la valeur est true, isAssigned indique que le badge a été attribué à un rôle et que le badge doit être affiché en tant que texte.

Si la valeur est false, est Affecté indique que le badge a été attribué pour un score gagné et que le badge doit être affiché en tant qu’image.

Toute modification de ce comportement doit être apportée dans un script personnalisé (remplacement ou recouvrement). Voir Personnalisation [côté](/help/communities/client-customize.md)client.

## Journal de débogage pour le score et le badge {#debug-log-for-scoring-and-badging}

Pour aider à déboguer le score et le badge, il est possible de configurer un fichier journal personnalisé. Le contenu de ce fichier journal peut alors être fourni au service clientèle si la fonction pose problème.

Pour obtenir des instructions détaillées, consultez [Créer un fichier](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)journal personnalisé.

Pour configurer rapidement un fichier slinglog :

1. Accédez à la prise en charge **du journal de la console Web** Adobe Experience Manager, par exemple

   * https://localhost:4502/system/console/slinglog

1. Sélectionner **Ajouter un nouveau journal**

   1. Sélectionner `DEBUG` pour le niveau de **journal**

   1. Entrez un nom pour le fichier **** journal, par exemple

      * logs/scoring-debug.log
   1. Entrer deux entrées **de journalisation** (classe) (à l&#39;aide de l&#39;icône `+` )

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. Sélectionnez **Enregistrer**



![debug-scoring-log](assets/debug-scoring-log.png)

Pour afficher les entrées de journal :

* Depuis la console Web

   * Sous le menu **État**
   * Sélectionner les fichiers **journaux**
   * Recherchez votre nom de fichier journal, tel que `scoring-debug`

* Sur le disque local du serveur

   * Le fichier journal se trouve sous &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * Par exemple, `.../crx-quickstart/logs/scoring-debug.log`

![journal de notation](assets/scoring-log.png)

## UGC pour le score et l&#39;insigne {#ugc-for-scoring-and-badging}

Il est possible de vue de l&#39;UGC en ce qui concerne la notation et l&#39;insigne lorsque le PSR choisi est JSRP ou MSRP, mais pas ASRP. (Si ces termes ne sont pas familiers, consultez Présentation [des Enregistrements](/help/communities/working-with-srp.md) de contenu [communautaire et des fournisseurs de ressources d’](/help/communities/srp.md)Enregistrement.)

Les descriptions d’accès aux données de score et de badge utilisent le JSRP, car l’UGC est facilement accessible en utilisant le [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP sur author**: l’expérimentation dans l’environnement d’auteur a pour effet d’afficher l’UGC uniquement à partir de l’environnement d’auteur.

**JSRP sur publication**: de même, si le test est effectué sur l’environnement de publication, il sera nécessaire d’accéder au CRXDE Lite avec des privilèges d’administration sur une instance de publication. Si l’instance de publication s’exécute en mode [de](/help/sites-administering/production-ready.md) production (nosamplecontent runmode), il sera nécessaire d’ [activer le CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

L&#39;emplacement de base de l&#39;UGC sur JSRP est `/content/usergenerated/asi/jcr/`.

### API de score et de badge {#scoring-and-badging-apis}

Les API suivantes sont disponibles pour utilisation :

* [com.adobe.cq.social.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.social.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

Les derniers Javadocs pour le pack de fonctionnalités installé sont disponibles pour les développeurs à partir du référentiel d’Adobes. Voir [Utilisation de Maven pour les communautés : Javadocs](/help/communities/maven.md#javadocs).

**L&#39;emplacement et le format de l&#39;UGC dans le référentiel peuvent être modifiés sans avertissement**.

### Exemple de configuration {#example-setup}

Les captures d’écran des données du référentiel proviennent de la configuration du score et du badge pour un forum sur deux sites AEM différents :

1. Un site AEM *avec* un identifiant unique (site communautaire créé à l’aide de l’assistant) :

   * Utilisation du site de didacticiel de prise en main créé lors du didacticiel de [prise en main](/help/communities/getting-started.md)
   * Localisation du noeud de la page du forum

      `/content/sites/engage/en/forum/jcr:content`

   * Ajouter les propriétés d’évaluation et de mise en badge

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * Localisation du noeud du composant de forum

      `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Ajouter la propriété d’affichage des badges

      `allowBadges = true`

   * Un utilisateur se connecte, crée un sujet de forum et reçoit un badge de bronze


1. Un site AEM *sans* identifiant unique :

   * Utilisation du guide des composants [de la communauté](/help/communities/components-guide.md)
   * Localisation du noeud de la page du forum

      `/content/community-components/en/forum/jcr:content`

   * Ajouter les propriétés d’évaluation et de mise en badge

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * Localisation du noeud du composant de forum

      `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Ajouter la propriété d’affichage des badges

      `allowBadges = true`

   * Un utilisateur se connecte, crée un sujet de forum et reçoit un badge de bronze


1. Un badge de modérateur est attribué à un utilisateur à l’aide de cURL :

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   Comme un utilisateur a gagné deux badges en bronze et qu&#39;il a reçu un badge de modérateur, c&#39;est ainsi que l&#39;utilisateur apparaît avec son entrée sur le forum.

   ![modérateur](assets/moderator.png)

>[!NOTE]
>
>Cet exemple ne suit pas les bonnes pratiques suivantes :
>
>* Les noms des règles de score doivent être globalement uniques ; ils ne devraient pas se terminer par le même nom.
>
>  
Voici un exemple de ce que *ne pas* faire :
>
>  /libs/settings/community/scoring/rules/site1/forums-score
>  /libs/settings/community/scoring/rules/site2/forums-score
>
>* Création d’images de badge uniques pour différents sites AEM


### Accès au score UGC {#access-scoring-ugc}

Il est préférable d’utiliser les [API](#scoring-and-badging-apis) .

À des fins d’enquête, à l’aide de JSRP pour l’exemple, le dossier de base contenant des scores est

* `/content/usergenerated/asi/jcr/scoring`

Le noeud enfant de `scoring` est le nom de la règle d’évaluation. Il est donc recommandé que les noms des règles d’évaluation sur un serveur soient globalement uniques.

Pour le site Interagir, l’utilisateur et son score se trouvent dans un chemin construit avec le nom de la règle de score, l’identifiant du site de la communauté ( `engage-ba81p`), un identifiant unique et l’identifiant de l’utilisateur :

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Pour le site du guide Composants de la communauté, l’utilisateur et son score se trouvent dans un chemin créé avec le nom de la règle de score, un id par défaut ( `default-site`), un id unique et l’id de l’utilisateur :

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

Le score est stocké dans la propriété `scoreValue_tl` qui peut directement contenir uniquement une valeur ou faire indirectement référence à un atomicCounter.

![access-score-ugc](assets/access-scoring-ugc.png)

### Insigne d&#39;accès UGC {#access-badging-ugc}

Il est préférable d’utiliser les [API](#scoring-and-badging-apis) .

À des fins d’enquête, à l’aide de JSRP, par exemple, le dossier de base contenant des informations sur les badges attribués ou attribués est

* `/content/usergenerated/asi/jcr`

Suivi du chemin d’accès au profil de l’utilisateur, qui se termine par un dossier de badges, tel que :

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Badge décerné {#awarded-badge}

![award-badging-ugc](assets/access-badging-ugc.png)

#### badge attribué {#assigned-badge}

![badge assigné](assets/assigned-badge.png)

## Informations supplémentaires {#additional-information}

Pour afficher une liste triée de membres en fonction des points :

* [Fonction](/help/communities/functions.md#leaderboard-function) du tableau de bord pour l’inclusion dans un site communautaire ou un modèle de groupe.
* [Composant](/help/communities/enabling-leaderboard.md)de tableau de bord, composant présenté de la fonction de tableau de bord, pour la création de pages.

