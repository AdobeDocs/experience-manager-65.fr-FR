---
title: Utilisation de contenu ciblé sur plusieurs sites
description: Si vous devez gérer du contenu ciblé, tel que des activités, des expériences et des offres sur vos différents sites, vous pouvez profiter de la prise en charge de sites multiples intégrée à AEM pour le contenu ciblé
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: 5e345ffd-4e9c-467f-8ebb-c798eeb61dea
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Multi Site Manager
role: User,Admin,Architect,Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '2838'
ht-degree: 99%

---

# Utilisation de contenu ciblé sur plusieurs sites{#working-with-targeted-content-in-multisites}

Si vous devez gérer du contenu ciblé, tel que des activités, des expériences et des offres sur vos différents sites, vous pouvez profiter de la prise en charge de sites multiples intégrée à AEM pour le contenu ciblé.

>[!NOTE]
>
>L’utilisation de contenu ciblé sur plusieurs sites est une fonctionnalité avancée. Pour utiliser cette fonctionnalité, vous devez connaître [Multi Site Manager](/help/sites-administering/msm.md) ainsi que l’[intégration d’Adobe Target](/help/sites-administering/target.md) à AEM.

Ce document contient les informations suivantes :

* Fournit une brève vue d’ensemble de la prise en charge multisite d’AEM pour le contenu ciblé.
* Décrit certains scénarios d’utilisation possibles sur la manière de lier des sites (dans une marque).
* Un exemple détaillé de l’utilisation que peuvent faire les spécialistes marketing de cette fonction
* Des instructions détaillées sur l’implémentation de la prise en charge de sites multiples pour le contenu ciblé.

Pour configurer la manière dont vos sites partagent du contenu personnalisé, vous devez effectuer les étapes suivantes :

1. [Créez une zone](#creating-new-areas) ou [créez une zone en tant que Live Copy](#creating-new-areas). Une zone comprend toutes les activités disponibles pour une *zone* de la page, c’est-à-dire l’emplacement sur la page où le composant est ciblé. La création d’une zone crée une zone vide, tandis que la création d’une zone en tant que Live Copy vous permet d’hériter du contenu entre les structures du site.

1. [Lier votre site ou votre page](#linking-sites-to-an-area) à une zone.

Vous pouvez à tout moment suspendre ou restaurer l’héritage. En outre, si vous ne souhaitez pas suspendre l’héritage, vous pouvez également créer des expériences locales. Par défaut, toutes les pages utilisent la zone principale, sauf indication contraire.

## Présentation de la prise en charge de sites multiples pour le contenu ciblé {#introduction-to-multisite-support-for-targeted-content}

La prise en charge de sites multiples pour le contenu ciblé est prête à l’emploi. Elle vous permet de pousser le contenu ciblé du gabarit que vous gérez via MSM vers une Live Copy locale ou de gérer des modifications globales et locales du contenu en question.

Vous gérez ces données dans une **zone**. Les zones délimitent le contenu ciblé (activités, expériences et offres) utilisé sur différents sites et fournissent un mécanisme reposant sur MSM afin de créer et de gérer l’héritage du contenu ciblé en même temps que l’héritage de site. Cela évite d’avoir à recréer du contenu ciblé dans les sites hérités, comme requis dans une version antérieure à AEM 6.2.

Au sein d’une zone, seules les activités associées à cette même zone sont poussées comme des Live Copies. Par défaut, la zone principale est sélectionnée. Une fois que vous avez créé des zones supplémentaires, vous pouvez les lier à vos sites ou pages pour indiquer le contenu ciblé qui est envoyé.

Un site ou une Live Copy est lié à une zone contenant les activités qui doivent être disponibles sur ce site ou cette Live Copy. Par défaut, le lien du site ou de la Live Copy est dirigé vers la zone principale, mais vous pouvez lier d’autres zones.

>[!NOTE]
>
>Tenez compte des points suivants lorsque vous utilisez la prise en charge multisite pour le contenu ciblé :
>
>* Lorsque vous utilisez des déploiements ou des Live Copy, une licence MSM est requise.
>* Lorsque vous utilisez la synchronisation avec Adobe Target, une licence Adobe Target est requise.
>

## Scénarios d’utilisation {#use-cases}

Selon votre cas d’utilisation, vous pouvez configurer la prise en charge multisite pour le contenu ciblé de différentes manières. Cette section décrit comment cela fonctionnerait théoriquement avec une seule marque. En outre, dans [Exemple : ciblage de contenu basé sur la géographie](#example-targeting-content-based-on-geography), vous pouvez découvrir une application réelle du ciblage de contenu sur plusieurs sites.

Le contenu ciblé est encapsulé dans ce que l’on appelle des zones qui définissent la portée des sites ou des pages. Ces zones sont définies au niveau de la marque. Une marque peut contenir plusieurs zones. Les zones peuvent être distinctes entre les marques. Bien qu’une marque ne contienne que la zone principale et soit donc partagée entre toutes les marques, une autre marque peut contenir plusieurs marques (par exemple, par zone géographique). Par conséquent, les marques n’ont pas besoin de refléter l’ensemble des zones entre elles.

Avec la prise en charge multisite pour le contenu ciblé, vous pouvez, par exemple, avoir deux sites (ou plus) avec **une** marque qui possède l’une des caractéristiques suivantes :

* Un ensemble complètement *distinct* de contenu ciblé. La modification du contenu ciblé sur un site n’a pas d’incidence sur l’autre site. Les sites qui sont liés à des zones distinctes écrivent et lisent sur leur propre zone configurée. Par exemple :

   * Le site A est lié à la zone X.
   * Le site B est lié à la zone Y

* Un ensemble *partagé* de contenu ciblé : la modification sur un site a un impact direct sur les deux sites. Cela est possible en configurant deux sites de façon à ce qu’ils fassent référence à la même zone. Les sites qui sont liés à la même zone partagent le contenu ciblé au sein de cette zone. Par exemple :

   * Le site A est lié à la zone X.
   * Le site B est lié à la zone X

* Un ensemble distinct de contenu ciblé *hérité* d’un autre site via MSM : le contenu peut être déployé, dans une seule direction, du maître vers la Live Copy. Par exemple :

   * Le site A est lié à la zone X.
   * Le site B est lié à la zone Y (qui est une Live Copy de la zone X).

**Plusieurs** marques peuvent être aussi utilisées sur un site, ce qui peut être plus complexe que cet exemple.

![chlimage_1-270](assets/chlimage_1-270.png)

>[!NOTE]
>
>Pour une approche plus technique de cette fonction, consultez la section [Structure de la gestion multisite pour le contenu ciblé](/help/sites-authoring/technical-multisite-targeted.md).

## Exemple : ciblage de contenu basé sur la géographie {#example-targeting-content-based-on-geography}

L’utilisation multisite pour le contenu ciblé vous permet de partager, de déployer ou d’isoler du contenu de personnalisation. Pour mieux illustrer l’utilisation de cette fonctionnalité, imaginez un scénario dans lequel vous souhaitez contrôler la manière dont le contenu ciblé est déployé en fonction de la géographie, par exemple :

Il existe quatre versions d’un même site en fonction de la géographie :

* Le site des **États-Unis** se trouve dans le coin supérieur gauche et constitue le site principal. Dans cet exemple, il est ouvert en mode Ciblage.
* Les trois autres versions de ce site sont les suivantes : **Canada**, **Grande-Bretagne** et **Australie**, qui sont toutes des Live Copy. Ces sites sont ouverts en mode Aperçu.

![chlimage_1-271](assets/chlimage_1-271.png)

Chaque site partage du contenu personnalisé dans des régions géographiques :

* Le Canada partage la zone principale avec les États-Unis.
* La Grande-Bretagne est liée à la zone européenne et hérite de la zone principale.
* L’Australie possède son propre contenu personnalisé, car elle se situe dans l’hémisphère sud et les produits de saison n’y sont pas pertinents.

![chlimage_1-272](assets/chlimage_1-272.png)

Pour l’hémisphère nord, une activité d’hiver a été créée, mais le spécialiste marketing en Amérique du Nord souhaiterait une image différente pour l’hiver pour le public masculin et il la modifie donc sur le site des États-Unis.

![chlimage_1-273](assets/chlimage_1-273.png)

Après avoir actualisé l’onglet, le site canadien passe automatiquement à la nouvelle image. Cela se produit parce qu’il partage la zone principale avec les États-Unis. L’image ne change pas sur les sites de la Grande-Bretagne et de l’Australie.

![chlimage_1-274](assets/chlimage_1-274.png)

Le ou la spécialiste du marketing souhaite déployer ces modifications dans la région européenne et [déploie la Live Copy](/help/sites-administering/msm-livecopy.md) en appuyant ou en cliquant sur **Page de déploiement**. Après actualisation de l’onglet, le site de la Grande-Bretagne dispose de la nouvelle image, car la région Europe hérite de la zone maître (après déploiement).

![chlimage_1-275](assets/chlimage_1-275.png)

L’image sur le site de l’Australie n’est pas affectée, ce qui est le comportement souhaité, car c’est l’été en Australie et le spécialiste marketing ne souhaite pas modifier ce contenu. Le site de l’Australie ne change pas, car il ne partage pas de zone avec une autre zone géographique et qu’il n’est pas une Live Copy d’une autre zone géographique. Le spécialiste marketing n’a pas à se soucier que le contenu ciblé du site australien soit remplacé.

En outre, pour la Grande-Bretagne, dont la zone est une Live Copy de la zone principale, vous pouvez voir le statut d’héritage grâce à l’indicateur vert à côté du nom de l’activité. Si une activité est héritée, vous ne pouvez pas la modifier, sauf si vous suspendez ou désolidarisez la Live Copy.

Vous pouvez à tout moment suspendre ou désolidariser complètement l’héritage. Vous pouvez également ajouter des expériences locales qui ne sont disponibles que pour cette expérience sans suspendre l’héritage.

>[!NOTE]
>
>Pour une approche plus technique de cette fonction, voir [Structure de la gestion de sites multiples pour le contenu ciblé](/help/sites-authoring/technical-multisite-targeted.md).

### Création d’une zone et création d’une zone en tant que Live Copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

Dans AEM, vous avez la possibilité de créer une zone ou de créer une zone en tant que Live Copy. La création d’une zone regroupe les activités et tout ce qui appartient à ces activités, comme les offres, les expériences, etc. Vous créez une zone lorsque vous souhaitez créer un ensemble complètement distinct de contenu ciblé ou partager un ensemble de contenu ciblé.

Si, toutefois, vous disposez d’un héritage configuré via le MSM entre les deux sites, vous pouvez hériter des activités. Dans ce cas, vous créez une zone en tant que Live Copy, où Y est une Live Copy de X et hérite donc également de toutes les activités.

>[!NOTE]
>
>Le déploiement par défaut déclenche des déploiements ultérieurs du contenu ciblé à chaque fois qu’une page est une Live Copy liée à une zone qui est également une Live Copy de la zone liée au plan directeur des pages.

Par exemple, dans le schéma suivant, deux des quatre sites partagent la zone maître (et toutes les activités qui font partie de cette zone), un site possède une zone qui est une Live Copy d’une zone de telle sorte qu’il partage les activités à mesure de leur déploiement et un autre site complètement distinct (qui nécessite par conséquent une zone pour ses activités).

![chlimage_1-276](assets/chlimage_1-276.png)

Pour réaliser cette action dans AEM, procédez comme suit :

* Le site A est lié à la zone principale. Aucune création de zone n’est nécessaire. La zone principale est sélectionnée par défaut dans AEM. Les sites A et B partagent des activités, etc.
* Le site B est lié à la zone principale. Aucune création de zone n’est nécessaire. La zone principale est sélectionnée par défaut dans AEM. Les sites A et B partagent des activités, etc.
* Le site C est lié à la zone héritée, qui est une Live Copy de la zone maître. Créez une zone comme Live Copy (avec une Live Copy reposant sur la zone maître). La zone héritée hérite des activités de la zone principale lors du déploiement.
* Le site D est lié à sa propre zone isolée. Créez une zone dans laquelle vous créez une zone entièrement nouvelle sans aucune activité encore définie. La zone isolée ne partage aucune activité avec un autre site.

## Création de zones {#creating-new-areas}

Les zones peuvent couvrir des activités et des offres. Après avoir créé une zone dans l’une d’elles (par exemple, les activités), la zone est également disponible dans l’autre (par exemple, les offres).

>[!NOTE]
>
>La zone par défaut appelée Zone principale est réduite par défaut lorsque vous cliquez sur le nom d’une marque **jusqu’à ce que** vous en créiez une autre. Ensuite, lorsque vous sélectionnez une marque dans la console **Activité** ou **Offres**, la console **Zone** s’affiche.

Pour créer une zone :

1. Accédez à **Personnalisation** > **Activités** ou **Offres** et sélectionnez ensuite votre marque.
1. Cliquez sur **Créer une zone**.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Cliquez sur l’icône **Zone**, puis sur **Suivant**.
1. Dans le champ **Titre**, saisissez le nom de la nouvelle zone. Vous pouvez également sélectionner des balises.
1. Cliquez sur **Créer**.

   AEM redirige vers la fenêtre de la marque, où elle répertorie toutes les zones créées. S’il existe une autre zone en plus de la zone principale, vous pouvez créer des zones directement dans la console Marque.

   ![chlimage_1-278](assets/chlimage_1-278.png)

## Création de zones comme Live Copy {#creating-areas-as-live-copies}

Vous créez une zone en tant que Live Copy pour hériter du contenu ciblé sur l’ensemble des structures du site.

Pour créer une zone comme Live Copy :

1. Accédez à **Personnalisation** > **Activités** ou **Offres** et sélectionnez ensuite votre marque.
1. Cliquez sur **Créer une zone comme Live Copy**.

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. Sélectionnez la zone dont vous souhaitez créer une Live Copy et cliquez sur **Suivant**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Dans le champ **Nom**, saisissez le nom de la Live Copy. Par défaut, les sous-pages sont incluses, mais vous pouvez les exclure en sélectionnant la case **Exclure les sous-pages**.

   ![chlimage_1-281](assets/chlimage_1-281.png)

1. Dans le menu déroulant **Configurations du déploiement**, sélectionnez la configuration appropriée.

   Pour obtenir une description de chaque option, consultez [Configurations de déploiement installées](/help/sites-administering/msm-sync.md#installed-rollout-configurations).

   Voir [Création et synchronisation des Live Copies](/help/sites-administering/msm-livecopy.md) pour plus d’informations sur les Live Copies.

   >[!NOTE]
   >
   >Lorsqu’une page est déployée sur une Live Copy et que la zone configurée pour la page Plan directeur est également le plan directeur de la zone configurée pour les pages Live Copy, la LiveAction **personalizationContentRollout** déclenche un subRollout synchrone, qui fait partie de la **configuration standard de déploiement**.

1. Cliquez sur **Créer**.

   AEM redirige vers la fenêtre de la marque, où elle répertorie toutes les zones créées. S’il existe une autre zone en plus de la zone principale, vous pouvez créer des zones directement à partir de la fenêtre de la marque.

   ![chlimage_1-282](assets/chlimage_1-282.png)

## Liaison de sites à une zone {#linking-sites-to-an-area}

Vous pouvez lier des zones à des pages ou à un site. Les zones sont héritées par toutes les sous-pages, sauf si ces pages sont superposées par un mappage sur une sous-page. Toutefois, les liens sont généralement établis au niveau du site.

Lorsque vous liez, seules les activités, expériences et offres de la zone sélectionnée sont disponibles. Cela évite la confusion accidentelle du contenu géré de manière indépendante. Si aucune autre zone n’est configurée, la zone principale de chaque marque est utilisée.

>[!NOTE]
>
>Les pages ou les sites faisant référence à la même zone utilisent le *même* ensemble partagé d’activités, d’expériences et d’offres. La modification d’une activité, d’une expérience ou d’une offre commune à plusieurs sites affecte tous les sites.

Pour lier un site à une zone :

1. Accédez au site (ou à la page) que vous souhaitez lier à une zone.
1. Sélectionnez le site ou la page, puis cliquez sur **Afficher les propriétés**.
1. Cliquez sur l’onglet **Personnalisation**.
1. Dans le menu **Marque**, sélectionnez la marque à laquelle vous souhaitez lier votre zone. Une fois la marque sélectionnée, les zones disponibles sont accessibles dans le menu **Référence de zone**.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Sélectionnez la zone dans le menu déroulant **Référence de zone** et cliquez sur **Enregistrer**.

   ![chlimage_1-284](assets/chlimage_1-284.png)

## Désolidarisation d’une Live Copy ou suspension de l’héritage du contenu ciblé {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Vous pouvez suspendre ou désolidariser l’héritage du contenu ciblé. La suspension ou la désolidarisation de la Live Copy est effectuée par activité. Par exemple, vous pouvez modifier des expériences dans votre activité, mais si cette activité est toujours liée à la copie héritée, vous ne pouvez pas modifier l’expérience ni les propriétés de l’activité.

La suspension de la Live Copy rompt temporairement l’héritage, mais vous pouvez ensuite le restaurer. La désolidarisation de la Live Copy rompt définitivement l’héritage.

Vous suspendez ou désolidarisez l’héritage du contenu ciblé en le restaurant dans une activité. Si une page ou un site est lié à une zone qui est une Live Copy, vous pouvez visualiser l’état d’héritage d’une activité.

Une activité qui hérite d’un autre site comporte une marque verte en regard de son nom. Un héritage suspendu est marqué en rouge et une activité créée localement ne comporte aucune icône.

>[!NOTE]
>
>* Vous pouvez uniquement suspendre ou désolidariser des Live Copies dans une activité.
>* Vous n’avez pas besoin de suspendre ou de désolidariser des Live Copies pour étendre une activité héritée. Vous pouvez toujours créer des **nouvelles** expériences et offres locales pour cette activité. Si vous souhaitez modifier une activité existante, vous devez suspendre l’héritage.
>

### Suspension de l’héritage {#suspending-inheritance}

Pour suspendre ou désolidariser l’héritage du contenu ciblé dans une activité :

1. Accédez à la page sur laquelle vous souhaitez désolidariser ou suspendre l’héritage et cliquez sur **Ciblage** dans le menu déroulant de mode.
1. Si votre page est liée à une zone qui est une Live Copy, vous pouvez voir le statut d’héritage. Cliquez sur **Commencer le ciblage**.
1. Pour suspendre une activité, effectuez l’une des opérations suivantes :

   1. Sélectionnez un élément de l’activité, tel que l’audience. AEM affiche automatiquement une boîte de confirmation Suspendre la Live Copy. (Vous pouvez suspendre la Live Copy en appuyant ou en cliquant sur un élément tout au long du processus de ciblage.)
   1. Sélectionnez **Suspendre la Live Copy** dans le menu déroulant de la barre d’outils.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Cliquez sur **Suspendre** pour suspendre l’activité. Les activités suspendues apparaissent en rouge.

   ![chlimage_1-286](assets/chlimage_1-286.png)

### Rupture de l’héritage {#breaking-inheritance}

Pour rompre l’héritage du contenu ciblé dans une activité :

1. Accédez à la page sur laquelle vous souhaitez désolidariser la Live Copy de la zone principale, puis cliquez sur **Ciblage** dans le menu déroulant du mode.
1. Si votre page est liée à une zone qui est une Live Copy, vous pouvez voir le statut d’héritage. Cliquez sur **Commencer le ciblage**.
1. Sélectionnez **Désolidariser une Live Copy** dans le menu déroulant de la barre d’outils. AEM confirme que vous souhaitez détacher la Live Copy.
1. Cliquez sur **Désolidariser** pour désolidariser la Live Copy de l’activité. Une fois la désolidarisation effectuée, le menu déroulant relatif à l’héritage disparaît. L’activité est désormais locale.

   ![chlimage_1-287](assets/chlimage_1-287.png)

## Restauration de l’héritage du contenu ciblé {#restoring-inheritance-of-targeted-content}

Si vous avez suspendu l’héritage du contenu ciblé dans une activité, vous pouvez le restaurer à tout moment. Cependant, si vous avez désolidarisé la Live Copy, vous ne pouvez pas restaurer l’héritage.

Pour restaurer l’héritage du contenu ciblé dans une activité :

1. Accédez à la page où vous souhaitez restaurer l’héritage et cliquez sur **Ciblage** dans le menu déroulant de mode.
1. Cliquez sur **Commencer le ciblage**.
1. Sélectionnez **Reprendre la Live Copy** dans le menu déroulant de la barre d’outils.

   ![chlimage_1-288](assets/chlimage_1-288.png)

1. Cliquez sur **Reprendre** pour confirmer que vous souhaitez reprendre l’héritage de la Live Copy. Toute modification apportée à l’activité actuelle est perdue si vous reprenez l’héritage.

## Suppression de zones {#deleting-areas}

Lorsque vous supprimez une zone, vous supprimez toutes les activités qu’elle contient. AEM vous avertit avant de pouvoir supprimer une zone. Si vous supprimez une zone à laquelle un site est lié, le mappage de cette marque sera automatiquement redéfini sur la zone maître.

Pour supprimer une zone :

1. Accédez à **Personnalisation** > **Activités** ou **Offres** et sélectionnez ensuite votre marque.
1. Cliquez sur l’icône en regard de la zone à supprimer.
1. Cliquez sur **Supprimer** et confirmez que vous souhaitez supprimer la zone.
