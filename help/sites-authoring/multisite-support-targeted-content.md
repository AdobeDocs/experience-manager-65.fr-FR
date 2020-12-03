---
title: Utilisation de contenu ciblé sur plusieurs sites
seo-title: Utilisation de contenu ciblé sur plusieurs sites
description: Si vous devez gérer du contenu ciblé, tel que des activités, des expériences et des offres sur vos différents sites, vous pouvez profiter de la prise en charge de sites multiples intégrée à AEM pour le contenu ciblé
seo-description: Si vous devez gérer du contenu ciblé, tel que des activités, des expériences et des offres sur vos différents sites, vous pouvez profiter de la prise en charge de sites multiples intégrée à AEM pour le contenu ciblé
uuid: acb2ffe1-d846-4580-bb69-d5af860796db
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 4dda6a03-d3ad-4e65-8b37-cee030fa4f7f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2906'
ht-degree: 100%

---


# Utilisation de contenu ciblé sur plusieurs sites{#working-with-targeted-content-in-multisites}

Si vous devez gérer du contenu ciblé, tel que des activités, des expériences et des offres sur vos différents sites, vous pouvez profiter de la prise en charge de sites multiples intégrée à AEM pour le contenu ciblé.

>[!NOTE]
>
>L’utilisation de contenu ciblé sur plusieurs sites est une fonctionnalité avancée. Pour utiliser cette fonctionnalité, vous devez connaître [Multi Site Manager](/help/sites-administering/msm.md) ainsi que l’[intégration d’Adobe Target](/help/sites-administering/target.md) à AEM.

Ce document fournit les éléments suivants :

* Une présentation succincte de la prise en charge de sites multiples sur AEM pour le contenu ciblé
* Plusieurs scénarios sur la façon dont vous pouvez lier des sites (sous une même marque)
* Un exemple détaillé de l’utilisation que peuvent faire les spécialistes marketing de cette fonction
* Des instructions détaillées sur l’implémentation de la prise en charge de sites multiples pour le contenu ciblé.

Pour définir la façon dont vos sites partagent du contenu personnalisé, vous devez effectuer les étapes suivantes :

1. [Créez une zone simple](#creating-new-areas) ou [créez une zone comme Live Copy](#creating-new-areas). Une zone comprend toutes les activités disponibles pour une *zone* de la page, c’est-à-dire l’emplacement sur la page où le composant est ciblé. La création d’une zone crée une zone vide, tandis que la création d’une zone comme Live Copy permet d’hériter du contenu sur l’ensemble des structures de site.

1. [Liez votre site ou page](#linking-sites-to-an-area) à une zone.

Vous pouvez à tout moment suspendre ou restaurer l’héritage. En outre, si vous ne souhaitez pas suspendre l’héritage, vous pouvez également créer des expériences locales. Sauf indication contraire, toutes les pages utilisent par défaut la zone maître.

## Présentation de la prise en charge de sites multiples pour le contenu ciblé     {#introduction-to-multisite-support-for-targeted-content}

La prise en charge de sites multiples pour le contenu ciblé est prête à l’emploi. Elle vous permet de pousser le contenu ciblé du gabarit que vous gérez via MSM vers une Live Copy locale ou de gérer des modifications globales et locales du contenu en question.

Vous gérez ces données dans une **zone**. Les zones délimitent le contenu ciblé (activités, expériences et offres) utilisé sur différents sites et fournissent un mécanisme reposant sur MSM afin de créer et de gérer l’héritage du contenu ciblé en même temps que l’héritage de site. De cette manière, il n’est plus nécessaire de recréer le contenu ciblé sur les sites hérités, comme c’était le cas dans les versions antérieures à AEM 6.2.

Au sein d’une zone, seules les activités associées à cette même zone sont poussées comme des Live Copies. Par défaut, la zone maître est sélectionnée. Une fois que vous avez créé d’autres zones, vous pouvez créer un lien vers vos sites ou pages afin d’indiquer le contenu ciblé qui doit être publié.

Un site ou une Live Copy présente un lien vers une zone contenant les activités qui doivent être disponibles sur le site ou la Live Copy en question. Par défaut, le lien du site ou de la Live Copy est dirigé vers la zone maître, mais vous pouvez lier d’autres zones.

>[!NOTE]
>
>Vous devez tenir compte des éléments suivants lorsque vous utilisez la prise en charge de sites multiples pour le contenu ciblé :
>
>* Lorsque vous utilisez des déploiements ou des Live Copies, une licence MSM est requise.
>* Lorsque vous utilisez la synchronisation avec Adobe Target, une licence Adobe Target est requise.
>



## Scénarios d’utilisation     {#use-cases}

Vous pouvez configurer la prise en charge de sites multiples pour le contenu ciblé de plusieurs manières, en fonction de vos besoins. Cette section décrit le fonctionnement théorique dans le cas d’une marque. En outre, dans [Exemple : ciblage de contenu basé sur la géographie](#example-targeting-content-based-on-geography), vous pouvez découvrir une application réelle du ciblage de contenu sur plusieurs sites.

Le contenu ciblé est enveloppé dans des zones qui définissent la portée des sites ou des pages. Ces zones sont définies au niveau de la marque. Une marque peut contenir plusieurs zones. Les zones peuvent différer entre les marques. Si une marque peut ne contenir qu’une zone maître et être ainsi partagée entre toutes les marques, une autre marque peut contenir plusieurs marques (par exemple, par région). Les marques, de ce fait, n’ont pas besoin de refléter les différentes zones entre elles.

Grâce à la prise en charge de sites multiples pour le contenu ciblé, vous pouvez, par exemple, disposer de deux sites (ou davantage) avec **une** marque présentant l’un des éléments suivants :

* Un ensemble complètement *distinct* de contenu ciblé. La modification du contenu ciblé sur un site n’a pas d’incidence sur l’autre site. Les sites qui sont liés à des zones distinctes écrivent et lisent sur leur propre zone configurée. Par exemple :

   * Le site A est lié à la zone X.
   * Le site B est lié à la zone Y.

* Un ensemble *partagé* de contenu ciblé : la modification sur un site a un impact direct sur les deux sites. Cela est possible en configurant deux sites de façon à ce qu’ils fassent référence à la même zone. Les sites qui sont liés à la même zone partagent le contenu ciblé au sein de cette zone. Par exemple :

   * Le site A est lié à la zone X.
   * Le site B est lié à la zone X.

* Un ensemble distinct de contenu ciblé *hérité* d’un autre site via MSM : le contenu peut être déployé, dans une seule direction, du maître vers la Live Copy. Par exemple :

   * Le site A est lié à la zone X.
   * Le site B est lié à la zone Y (qui est une Live Copy de la zone X).

Vous pouvez également avoir **plusieurs** marques utilisées sur un même site, qui peuvent être plus complexes que cet exemple.

![chlimage_1-270](assets/chlimage_1-270.png)

>[!NOTE]
>
>Pour une approche plus technique de cette fonction, voir [Structure de la gestion de sites multiples pour le contenu ciblé](/help/sites-authoring/technical-multisite-targeted.md).

## Exemple : ciblage de contenu basé sur la géographie {#example-targeting-content-based-on-geography}

L’utilisation de sites multiples pour le contenu ciblé permet de partager, de déployer ou d’isoler le contenu personnalisé. Pour mieux illustrer l’utilisation de cette fonction, supposons que vous souhaitiez contrôler la manière dont le contenu ciblé est déployé en fonction de la zone géographique, comme dans le scénario suivant :

Il existe quatre versions du même site en fonction de la zone géographique :

* Le site des **États-Unis** se situe dans le coin supérieur gauche et constitue le site principal. Dans cet exemple, il est ouvert en mode Ciblage.
* Les trois autres versions de ce site sont **Canada**, **Grande-Bretagne** et **Australie** et ce sont toutes des Live Copies. Ces sites sont ouverts en mode Aperçu.

![chlimage_1-271](assets/chlimage_1-271.png)

Chaque site partage du contenu personnalisé dans des zones géographiques :

* Le Canada partage la zone maître avec les États-Unis.
* La Grande-Bretagne est liée à la zone européenne et hérite de la zone maître.
* L’Australie possède son propre contenu personnalisé, car elle se situe dans l’hémisphère sud et les produits de saison n’y sont pas pertinents.

![chlimage_1-272](assets/chlimage_1-272.png)

Pour l’hémisphère nord, une activité d’hiver a été créée, mais le spécialiste marketing en Amérique du Nord souhaiterait une image différente pour l’hiver pour le public masculin et il la modifie donc sur le site des États-Unis.

![chlimage_1-273](assets/chlimage_1-273.png)

Après actualisation de l’onglet, la nouvelle image est appliquée sur le site canadien sans action de notre part. Cela est dû au fait que le Canada partage sa zone maître avec les États-Unis. L’image ne change pas sur les sites de la Grande-Bretagne et de l’Australie.

![chlimage_1-274](assets/chlimage_1-274.png)

Le marketeur souhaite déployer ces modifications dans la région européenne et [déploie la Live Copy](/help/sites-administering/msm-livecopy.md) en appuyant ou en cliquant sur **Page de déploiement**. Après actualisation de l’onglet, le site de la Grande-Bretagne dispose de la nouvelle image, car la région Europe hérite de la zone maître (après déploiement).

![chlimage_1-275](assets/chlimage_1-275.png)

L’image sur le site de l’Australie n’est pas affectée, ce qui est le comportement souhaité, car c’est l’été en Australie et le spécialiste marketing ne souhaite pas modifier ce contenu. Le site de l’Australie ne change pas puisqu’il ne partage pas de zone avec une autre région et qu’il n’est pas une Live Copy d’une autre région. Le spécialiste marketing n’a pas à se soucier que le contenu ciblé du site australien soit remplacé.

En outre, pour la Grande-Bretagne, dont la zone est une Live Copy de la zone maître, vous pouvez voir l’état d’héritage à l’aide de l’indicateur vert en regard du nom de l’activité. Si une activité est héritée, vous ne pouvez pas la modifier, sauf si vous suspendez ou désolidarisez la Live Copy.

Vous pouvez à tout moment suspendre l’héritage ou désolidariser complètement l’héritage. En outre, vous pouvez toujours ajouter des expériences locales qui sont uniquement disponibles dans cette expérience sans suspendre l’héritage.

>[!NOTE]
>
>Pour une approche plus technique de cette fonction, voir [Structure de la gestion de sites multiples pour le contenu ciblé](/help/sites-authoring/technical-multisite-targeted.md).

### Comparaison de la création d’une zone simple et de la création d’une zone comme Live Copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

Dans AEM, vous avez la possibilité de simplement créer une zone ou de la créer comme Live Copy. La création d’une zone permet de regrouper les activités et tout ce qui appartient à ces activités, comme les offres, les expériences, etc. Vous créez une zone lorsque vous souhaitez créer un ensemble complètement distinct de contenu ciblé ou lorsque vous souhaitez partager un ensemble de contenu ciblé.

Cependant, si vous disposez d’un héritage configuré entre les deux sites via MSM, vous pouvez choisir d’hériter des activités. Dans ce cas, vous créez une zone comme Live Copy, où Y est une Live Copy de X et hérite donc également de toutes les activités.

>[!NOTE]
>
>Le déploiement par défaut déclenche des déploiements ultérieurs du contenu ciblé à chaque fois qu’une page est une Live Copy liée à une zone qui est également une Live Copy de la zone liée au plan directeur des pages.

Par exemple, dans le schéma suivant, deux des quatre sites partagent la zone maître (et toutes les activités qui font partie de cette zone), un site possède une zone qui est une Live Copy d’une zone de telle sorte qu’il partage les activités à mesure de leur déploiement et un autre site complètement distinct (qui nécessite par conséquent une zone pour ses activités).

![chlimage_1-276](assets/chlimage_1-276.png)

Pour mettre en place cette configuration dans AEM, procédez comme suit :

* Le site A est lié à la zone maître et aucune zone ne doit être créée. La zone maître est sélectionnée par défaut dans AEM. Les sites A et B partagent les activités, etc.
* Le site B est lié à la zone maître et aucune zone ne doit être créée. La zone maître est sélectionnée par défaut dans AEM. Les sites A et B partagent les activités, etc.
* Le site C est lié à la zone héritée, qui est une Live Copy de la zone maître. Créez une zone comme Live Copy (avec une Live Copy reposant sur la zone maître). La zone héritée hérite des activités de la zone maître lors du déploiement.
* Le site D est lié à sa propre zone isolée. Créez une zone complètement nouvelle sans aucune activité définie. La zone isolée ne partagera les activités avec aucun autre site.

## Création de zones     {#creating-new-areas}

Les zones peuvent couvrir les activités et les offres. Après avoir créé une zone dans l’une d’entre elles (par exemple, les activités), la zone devient également disponible dans l’autre (par exemple, les offres).

>[!NOTE]
>
>La zone par défaut appelée Zone principale est réduite par défaut lorsque vous appuyez ou cliquez sur le nom d’une marque **jusqu’à ce que** vous en créiez une autre. Ensuite, lorsque vous sélectionnez une marque dans la console **Activité** ou **Offres**, la console **Zone** s’affiche.

Pour créer une zone :

1. Accédez à **Personnalisation** > **Activités** ou **Offres** et sélectionnez ensuite votre marque.
1. Appuyez ou cliquez sur **Créer une zone**.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Cliquez sur l’icône **Zone** puis cliquez sur **Suivant**.
1. Dans le champ **Titre**, saisissez le nom de la nouvelle zone. Vous pouvez également sélectionner des balises si vous le souhaitez.
1. Appuyez ou cliquez sur **Créer**.

   AEM vous redirige vers la fenêtre de marque, où il répertorie toutes les zones créées. S’il existe une autre zone que la zone maître, vous pouvez alors créer des zones directement dans la console Marque.

   ![chlimage_1-278](assets/chlimage_1-278.png)

## Création de zones comme Live Copies {#creating-areas-as-live-copies}

Vous créez une zone comme Live Copy afin d’hériter du contenu ciblé à travers les structures de site.

Pour créer une zone comme Live Copy :

1. Accédez à **Personnalisation** > **Activités** ou **Offres** et sélectionnez ensuite votre marque.
1. Appuyez ou cliquez sur **Créer une zone comme Live Copy**.

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. Sélectionnez la zone dont vous souhaitez créer une Live Copy et cliquez sur **Suivant**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Dans le champ **Nom**, saisissez le nom de la Live Copy. Par défaut, les sous-pages sont incluses, mais vous pouvez les exclure en sélectionnant la case **Exclure les sous-pages**.

   ![chlimage_1-281](assets/chlimage_1-281.png)

1. Dans le menu déroulant **Configurations du déploiement**, sélectionnez la configuration appropriée.

   Voir [Configurations de déploiement installées](/help/sites-administering/msm-sync.md#installed-rollout-configurations) pour obtenir une description de chaque option.

   Voir [Création et synchronisation des Live Copies](/help/sites-administering/msm-livecopy.md) pour plus d’informations sur les Live Copies.

   >[!NOTE]
   >
   >Lorsqu’une page est déployée sur une Live Copy et que la zone configurée pour la page Plan directeur est également le plan directeur de la zone configurée pour les pages Live Copy, la LiveAction **personalizationContentRollout** déclenche un subRollout synchrone, qui fait partie de la **configuration standard de déploiement**.

1. Appuyez ou cliquez sur **Créer**.

   AEM vous redirige vers la fenêtre de marque, où il répertorie toutes les zones créées. S’il existe une autre zone que la zone maître, vous pouvez alors créer des zones directement dans la fenêtre de marque.

   ![chlimage_1-282](assets/chlimage_1-282.png)

## Liaison de sites à une zone {#linking-sites-to-an-area}

Vous pouvez lier des zones à des pages ou à un site. Les zones sont héritées par toutes les sous-pages à moins que ces pages ne soient recouvertes par un mappage sur une sous-page. Toutefois, les liens sont généralement établis au niveau du site.

Lorsque vous définissez un lien, seules les activités, expériences et offres de la zone sélectionnée sont disponibles. Cela permet d’éviter toute confusion accidentelle avec le contenu géré indépendamment. Si aucune autre zone n’est configurée, la zone maître de chaque marque est utilisée.

>[!NOTE]
>
>Les pages ou les sites faisant référence à la même zone utilisent le *même* ensemble partagé d’activités, d’expériences et d’offres. La modification d’une activité, d’une expérience ou d’une offre commune à plusieurs sites affecte tous les sites.

Pour lier un site à une zone :

1. Accédez au site (ou à la page) que vous souhaitez lier à une zone.
1. Sélectionnez le site ou la page et appuyez ou cliquez ensuite sur **Afficher les propriétés**.
1. Appuyez ou cliquez sur l’onglet **Personnalisation**.
1. Dans le menu **Marque**, sélectionnez la marque à laquelle vous souhaitez lier votre zone. Après avoir sélectionné la marque, les zones disponibles figurent dans le menu **Référence de zone**.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Sélectionnez la zone dans le menu déroulant **Référence de zone** et appuyez ou cliquez sur **Enregistrer**.

   ![chlimage_1-284](assets/chlimage_1-284.png)

## Désolidarisation d’une Live Copy ou suspension de l’héritage du contenu ciblé {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Vous pouvez suspendre ou désolidariser l’héritage du contenu ciblé. La suspension ou la désolidarisation de la Live Copy se fait par activité. Par exemple, si vous souhaitez modifier des expériences de votre activité et que cette activité est toujours liée à la copie héritée, vous ne pouvez pas modifier l’expérience ni aucune autre propriété de cette activité.

La suspension de la Live Copy rompt temporairement l’héritage, mais vous pouvez ensuite le restaurer. Quant à elle, la désolidarisation de la Live Copy rompt définitivement l’héritage.

Vous suspendez ou désolidarisez l’héritage du contenu ciblé en le restaurant dans une activité. Si une page ou un site est lié à une zone qui est une Live Copy, vous pouvez visualiser l’état d’héritage d’une activité.

Une activité qui hérite d’un autre site comporte une marque verte en regard de son nom. Un héritage suspendu est indiqué en rouge, alors qu’une activité créée localement n’a aucune icône.

>[!NOTE]
>
>* Vous pouvez uniquement suspendre ou désolidariser des Live Copies dans une activité.
>* Vous n’avez pas besoin de suspendre ou de désolidariser des Live Copies pour étendre une activité héritée. Vous pouvez toujours créer de **nouvelles** expériences et offres locales pour cette activité. Si vous souhaitez modifier une activité existante, il vous faut suspendre l’héritage.
>



### Suspension de l’héritage     {#suspending-inheritance}

Pour suspendre ou désolidariser l’héritage du contenu ciblé dans une activité :

1. Accédez à la page sur laquelle vous souhaitez désolidariser ou suspendre l’héritage et appuyez ou cliquez sur **Ciblage** dans le menu déroulant de mode.
1.  Si votre page est liée à une zone qui est une Live Copy, vous pouvez voir l’état d’héritage. Appuyez ou cliquez sur **Commencer le ciblage**.
1. Pour suspendre une activité, effectuez l’une des opérations suivantes :

   1. Sélectionnez un élément de l’activité, tel que le public. AEM affiche automatiquement une fenêtre de confirmation Suspendre la Live Copy. (Vous pouvez suspendre la Live Copy en appuyant ou en cliquant sur n’importe quel élément du processus de ciblage.)
   1. Sélectionnez **Suspendre la Live Copy** dans le menu déroulant de la barre d’outils.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Appuyez ou cliquez sur **Suspendre** pour suspendre l’activité. Les activités suspendues apparaissent en rouge.

   ![chlimage_1-286](assets/chlimage_1-286.png)

### Rompre l’héritage {#breaking-inheritance}

Pour rompre l’héritage du contenu ciblé dans une activité :

1. Accédez à la page sur laquelle vous souhaitez désolidariser la Live Copy du gabarit et appuyez ou cliquez sur **Ciblage** dans le menu déroulant de mode.
1.  Si votre page est liée à une zone qui est une Live Copy, vous pouvez voir l’état d’héritage. Appuyez ou cliquez sur **Commencer le ciblage**.
1. Sélectionnez **Désolidariser une Live Copy** dans le menu déroulant de la barre d’outils. AEM confirme que vous souhaitez détacher la Live Copy.
1. Appuyez ou cliquez sur **Désolidariser** pour désolidariser la Live Copy de l’activité. Une fois la désolidarisation effectuée, le menu déroulant relatif à l’héritage disparaît. L’activité est maintenant une activité locale.

   ![chlimage_1-287](assets/chlimage_1-287.png)

## Restauration de l’héritage du contenu ciblé {#restoring-inheritance-of-targeted-content}

Si vous avez suspendu l’héritage du contenu ciblé dans une activité, vous pouvez le restaurer à tout moment. Cependant, si vous avez désolidarisé la Live Copy, vous ne pouvez pas restaurer l’héritage.

Pour restaurer l’héritage du contenu ciblé dans une activité :

1. Accédez à la page sur laquelle vous souhaitez restaurer l’héritage et appuyez ou cliquez sur **Ciblage** dans le menu déroulant de mode.
1. Appuyez ou cliquez sur **Commencer le ciblage**.
1. Sélectionnez **Reprendre la Live Copy** dans le menu déroulant de la barre d’outils.

   ![chlimage_1-288](assets/chlimage_1-288.png)

1. Appuyez ou cliquez sur **Reprendre** pour confirmer que vous souhaitez reprendre l’héritage de Live Copy. Toutes les modifications apportées à l’activité en cours sont perdues si vous reprenez l’héritage.

## Suppression de zones     {#deleting-areas}

Lorsque vous supprimez une zone, vous supprimez toutes les activités au sein de cette zone. AEM vous avertit avant toute suppression de zone. Si vous supprimez une zone à laquelle un site est lié, le mappage de cette marque sera automatiquement redéfini sur la zone maître.

Pour supprimer une zone :

1. Accédez à **Personnalisation** > **Activités** ou **Offres** et sélectionnez ensuite votre marque.
1. Appuyez ou cliquez sur l’icône située en regard de la zone que vous souhaitez supprimer.
1. Appuyez ou cliquez sur **Supprimer** et confirmez que vous souhaitez supprimer la zone.

