---
title: Scores et insignes essentiels
seo-title: Scores et insignes essentiels
description: Présentation de la fonctionnalité Scores et badges
seo-description: Présentation de la fonctionnalité Scores et badges
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
translation-type: tm+mt
source-git-commit: d522c5ec6c72a9fd391d021f2fac37f88c686bd9

---


# Scores et insignes essentiels{#scoring-and-badges-essentials}

La fonction de notation et de badges des communautés AEM permet d’identifier et de récompenser les membres de la communauté.

Les détails de la configuration de la fonctionnalité sont décrits dans la section

* [Score et badges des communautés](/help/communities/implementing-scoring.md)

Cette page contient des détails techniques supplémentaires :

* comment [afficher un badge](#displaying-badges) sous forme d’image ou de texte
* comment activer la journalisation [de débogage étendue](#debug-log-for-scoring-and-badging)
* comment [accéder à l&#39;UGC](#ugc-for-scoring-and-badging) en ce qui concerne la notation et le badge

>[!CAUTION]
>
>La structure d’implémentation visible dans CRXDE Lite peut être modifiée.

## Affichage des badges {#displaying-badges}

Le contrôle d’un badge affiché sous forme de texte ou d’image côté client dans le modèle HBS est activé.

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

Si la valeur est true, isAssigned indique que le badge a été affecté à un rôle et que le badge doit être affiché sous forme de texte.

Si la valeur est false, est Attribué indique que le badge a été attribué pour un score gagné et que le badge doit être affiché sous forme d’image.

Toute modification de ce comportement doit être apportée dans un script personnalisé (remplacement ou recouvrement). Voir Personnalisation [côté](/help/communities/client-customize.md)client.

## Journal de débogage pour le score et le badge {#debug-log-for-scoring-and-badging}

Pour faciliter le débogage du score et du badge, vous pouvez configurer un fichier journal personnalisé. Le contenu de ce fichier journal peut alors être fourni au service clientèle en cas de problème avec la fonctionnalité.

Pour obtenir des instructions détaillées, consultez [Création d’un fichier](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)journal personnalisé.

Pour configurer rapidement un fichier slinglog :

1. accéder à la prise en charge **du journal de la console Web** Adobe Experience Manager, par exemple

   * https://localhost:4502/system/console/slinglog

1. sélectionner **Ajouter un nouveau journal**

   1. sélectionner `DEBUG`pour le niveau **journal**

   1. saisissez un nom pour le fichier **** journal, par exemple

      * logs/scoring-debug.log
   1. saisissez deux entrées **Logger **(class) (à l’aide d’une `+` icône)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. sélectionnez **Enregistrer**



![chlimage_1-193](assets/chlimage_1-193.png)

Pour afficher les entrées du journal

* depuis la console Web

   * sous le **menu État **menu
   * sélectionner **Fichiers journaux**
   * recherchez le nom du fichier journal, par exemple `scoring-debug`

* sur le disque local du serveur

   * le fichier journal se trouve sous &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * par exemple, `.../crx-quickstart/logs/scoring-debug.log`

![chlimage_1-194](assets/chlimage_1-194.png)

## UGC pour le score et le badge {#ugc-for-scoring-and-badging}

Il est possible d’afficher l’UGC en ce qui concerne la notation et la notation lorsque le SRP choisi est JSRP ou MSRP, mais pas ASRP. (Si vous ne connaissez pas ces termes, consultez Présentation [du fournisseur de ressources de stockage](/help/communities/working-with-srp.md) et de [stockage de contenu de la](/help/communities/srp.md)communauté.)

Les descriptions d’accès aux données de score et de badge utilisent JSRP, car l’UGC est facilement accessible à l’aide de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP sur l&#39;auteur** : l’expérimentation dans l’environnement d’auteur entraîne l’affichage de l’UGC uniquement à partir de l’environnement d’auteur.

**JSRP sur la publication** : de même, si vous effectuez des tests sur l’environnement de publication, il sera nécessaire d’accéder à CRXDE Lite avec des droits d’administrateur sur une instance de publication. Si l’instance de publication s’exécute en mode [de](/help/sites-administering/production-ready.md) production (mode d’exécution nosamplecontent), il sera nécessaire d’ [activer CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

L’emplacement de base de l’UGC sur JSRP est `/content/usergenerated/asi/jcr/`.

### API de score et de badge {#scoring-and-badging-apis}

Les API suivantes peuvent être utilisées :

* [com.adobe.cq.social.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.social.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

Les derniers Javadocs pour le Feature Pack installé sont accessibles aux développeurs à partir du référentiel Adobe. Voir [Utilisation de Maven pour les communautés : Javadocs](/help/communities/maven.md#javadocs).

**L’emplacement et le format de l’UGC dans le référentiel peuvent être modifiés sans avertissement**.

### Exemple de configuration {#example-setup}

Les captures d’écran des données du référentiel proviennent de la configuration du score et du badge pour un forum sur deux sites AEM différents :

1. Un site AEM *avec* un identifiant unique (site de la communauté créé à l’aide de l’assistant) :

* utilisation du site Didacticiel de prise en main (engager) créé pendant le didacticiel de [prise en main](/help/communities/getting-started.md)
* localiser le noeud de la page du forum

   * `/content/sites/engage/en/forum/jcr:content`

* ajout de propriétés d’évaluation et de mise en badge

   ```
   scoringRules = [/etc/community/scoring/rules/comments-scoring,
   /etc/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/etc/community/badging/rules/comments-scoring,
   /etc/community/badging/rules/forums-scoring]
   ```

* localiser le noeud du composant de forum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

* ajouter une propriété pour afficher les badges

   * `allowBadges = true`

* un utilisateur se connecte, crée un sujet de forum et reçoit un badge de bronze

1. Un site AEM *sans* ID unique :

* utilisation du guide des composants [de la communauté](/help/communities/components-guide.md)
* localiser le noeud de la page du forum

   * `/content/community-components/en/forum/jcr:content`

* ajout de propriétés d’évaluation et de mise en badge

   ```
   scoringRules = [/etc/community/scoring/rules/comments-scoring,
   /etc/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/etc/community/badging/rules/comments-scoring,
   /etc/community/badging/rules/forums-scoring]
   ```

* localiser le noeud du composant de forum

   * `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

* ajouter une propriété pour afficher les badges

   * `allowBadges = true`

* un utilisateur se connecte, crée un sujet de forum et reçoit un badge de bronze

1. un badge de modérateur est attribué à un utilisateur à l’aide de cURL :

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/etc/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
```

Comme un utilisateur a obtenu deux badges en bronze et qu&#39;il a reçu un badge de modérateur, voici comment l&#39;utilisateur apparaît avec son entrée sur le forum :

![chlimage_1-195](assets/chlimage_1-195.png)

>[!NOTE]
>
>Cet exemple ne suit pas les bonnes pratiques suivantes :
>
>* les noms des règles de notation doivent être uniques au niveau mondial ; ils ne doivent pas se terminer par le même nom.
   >  Un exemple de ce que *ne pas *faire :
   >  /etc/community/score/rule/site1/forums-score
   >  /etc/community/score/rule/site2/forums-score
   >
   >
* création d’images de badge uniques pour différents sites AEM
>



### Accès au score UGC {#access-scoring-ugc}

Il est préférable d’utiliser les [API](#scoring-and-badging-apis) .

À des fins d’enquête, à l’aide de JSRP pour l’exemple, le dossier de base contenant les scores est

* `/content/usergenerated/asi/jcr/scoring`

Le noeud enfant de `scoring`est le nom de la règle de notation. Il est donc recommandé que les noms des règles de notation sur un serveur soient globalement uniques.

Pour le site Geometrixx Engage, l’utilisateur et son score se trouvent dans un chemin construit avec le nom de la règle de notation, l’identifiant du site de la communauté ( `engage-ba81p`), un identifiant unique et l’identifiant de l’utilisateur :

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Pour le site de guide Composants de la communauté, l’utilisateur et son score se trouvent dans un chemin construit avec le nom de la règle de notation, un ID par défaut ( `default-site`), un ID unique et l’ID de l’utilisateur :

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

Le score est stocké dans la propriété `scoreValue_tl` qui peut directement contenir uniquement une valeur ou indirectement faire référence à un atomicCounter.

![chlimage_1-196](assets/chlimage_1-196.png)

### Insigne d&#39;accès UGC {#access-badging-ugc}

Il est préférable d’utiliser les [API](#scoring-and-badging-apis) .

À des fins d’enquête, à l’aide de JSRP, par exemple, le dossier de base contenant des informations sur les badges attribués ou attribués est

* /content/usergenerate/asi/jcr

Suivi du chemin d’accès au profil de l’utilisateur, se terminant par un dossier de badges, tel que

* /home/users/community/w271OOup2Z4DjnOQrviv/profile/badges

#### badge décerné {#awarded-badge}

![chlimage_1-197](assets/chlimage_1-197.png)

#### badge attribué {#assigned-badge}

![chlimage_1-198](assets/chlimage_1-198.png)

## Informations supplémentaires {#additional-information}

Pour afficher une liste triée de membres en fonction des points :

* [Fonction](/help/communities/functions.md#leaderboard-function) du tableau de bord pour l’inclusion dans un site communautaire ou un modèle de groupe.
* [Composant](/help/communities/enabling-leaderboard.md)de classement, composant incitatif de la fonction de classement, pour la création de pages.

