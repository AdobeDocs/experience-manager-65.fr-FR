---
title: Intégration aux bonnes pratiques de Adobe Creative Cloud
description: Bonnes pratiques d’intégration [!DNL Adobe Experience Manager] avec [!DNL Adobe Creative Cloud] pour rationaliser les workflows de transfert de ressources et obtenir une vitesse de contenu élevée.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '3280'
ht-degree: 58%

---

# [!DNL Adobe Experience Manager] et [!DNL Creative Cloud] bonnes pratiques d’intégration {#aem-and-creative-cloud-integration-best-practices}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices.html?lang=en) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/aem-cc-integration-best-practices.html?lang=en) |

[!DNL Adobe Experience Manager Assets] est une solution de gestion des ressources numériques (DAM) qui peut s’intégrer à [!DNL Adobe Creative Cloud] pour aider les utilisateurs de la gestion des actifs numériques à collaborer avec les équipes créatives, en rationalisant la collaboration dans le processus de création de contenu.

[!DNL Adobe Creative Cloud] offre aux équipes créatives un écosystème de solutions et de services pour leur permettre de créer des ressources numériques. Il comprend les applications de bureau et mobiles, les services cloud tels que le stockage avec synchronisation de bureau ou l’expérience web, ainsi que des plateformes marketing telles que [!DNL Adobe Stock].

Lisez ce qui suit pour savoir quelles intégrations choisir entre poste de travail et DAM d’entreprise selon votre cas d’utilisation et découvrir quelles sont les bonnes pratiques associées aux workflows de connexion.

>[!NOTE]
>
>[!DNL Experience Manager] to [!DNL Creative Cloud] le partage de dossiers est obsolète et n’est plus traité dans ce guide. Adobe recommande d’utiliser des fonctionnalités plus récentes, telles que [Adobe d’un lien de ressource](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html) ou [application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html) pour permettre à l’utilisateur créatif d’accéder aux ressources gérées dans [!DNL Experience Manager].

## Besoins en matière de collaboration des créatifs, des marketeurs et des utilisateurs de la gestion des ressources numériques {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Conditions requises | Cas d’utilisation | Surfaces impliquées |
|---|---|---|
| Simplifier l’expérience pour les créatifs utilisant un poste de travail | Simplifiez l’accès aux ressources depuis une gestion des ressources numériques ([!DNL Experience Manager Assets]) pour les créatifs ou, plus largement, pour les utilisateurs sur poste de travail utilisant des applications de création de ressources natives. Ils ont besoin d’une méthode simple et simple pour découvrir, utiliser (ouvrir), modifier et enregistrer les modifications dans [!DNL Experience Manager], ainsi que de charger de nouveaux fichiers. | Poste de travail Windows ou Mac ; [!DNL Creative Cloud] apps |
| Fournir des ressources de grande qualité, prêtes à l’emploi depuis [!DNL Adobe Stock] | Les spécialistes marketing accélèrent le processus de création de contenu en contribuant à la recherche et à la découverte de ressources. Les créatifs utilisent les ressources approuvées directement dans leurs outils de création. | [!DNL Experience Manager Assets] ; marketplace [!DNL Adobe Stock] ; champs de métadonnées |
| Distribution et partage de ressources par sociétés | Les services internes/succursales locales et les partenaires externes, les distributeurs et les agences utilisent les ressources approuvées, partagées par la société mère. La société souhaite partager de manière sécurisée et transparente les ressources créées pour une réutilisation plus large. | Brand Portal, Asset Share Commons |

## Offres d’Adobe pour répondre aux besoins en matière de collaboration {#adobe-offerings-to-support-the-collaboration-need}

| Proposition de valeur pour les personnes impliquées | Offre d’Adobe | Surfaces impliquées |
|---|---|---|
| Les utilisateurs créatifs découvrent des ressources à partir de [!DNL Experience Manager], ouvrez-les et utilisez-les, modifiez et chargez les modifications dans [!DNL Experience Manager], ainsi que de charger de nouveaux fichiers dans [!DNL Experience Manager], sans quitter [!DNL Creative Cloud] applications. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] et [!DNL Adobe InDesign]. |
| Les utilisateurs professionnels simplifient l’ouverture et l’utilisation des ressources, la modification et le chargement des modifications dans [!DNL Experience Manager] et le chargement de nouveaux fichiers dans [!DNL Experience Manager] à partir de l’environnement de poste de travail. Ils utilisent une intégration générique pour ouvrir n’importe quel type de ressource dans l’application de bureau native, y compris les applications autres qu’Adobe. | [Application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager]Application de bureau sous Windows et Mac |
| Les marketeurs et les utilisateurs professionnels découvrent, prévisualisent, attribuent des licences et enregistrent et gèrent les [!DNL Adobe Stock] ressources de [!DNL Experience Manager]. Les ressources sous licence et enregistrées fournissent une sélection [!DNL Adobe Stock] métadonnées pour une meilleure gouvernance. | [Intégration d’Experience Manager et d’Adobe Stock](aem-assets-adobe-stock.md) | Interface web [!DNL Experience Manager] |

Cet article se concentre principalement sur les deux premiers aspects des besoins de collaboration. La distribution et la source des ressources à grande échelle sont brièvement mentionnées comme cas d’utilisation. Pour répondre à ces besoins, pensez à Adobe Brand Portal ou à Asset Share Commons. Autres solutions, telles que [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=fr), solutions qui peuvent être créées à partir de [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) composants, [Partage de liens](/help/assets/link-sharing.md), à l’aide de [Experience Manager Assets](/help/assets/manage-assets.md) doivent être examinées en fonction de besoins spécifiques.

![Connexions de Creative Cloud pour Experience Manager, choisissez la fonctionnalité à utiliser](assets/creative-connections-aem.png)

### Correspondance des cas d’utilisation aux solutions Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Cas d’utilisation | [!DNL Adobe Asset Link] | Appli de bureau [!DNL Experience Manager] | Remarques/autres solutions |
|---|---|---|---|
| Discover - parcourir les dossiers DAM | Oui | [!DNL Experience Manager] Actions de bureau et de l’interface web |  |
| Discover - Accès aux collections DAM | Oui | [!DNL Experience Manager] Actions de bureau et de l’interface web |  |
| Discover : recherche de ressources à partir de la gestion des ressources numériques | Oui | [!DNL Experience Manager] Actions de bureau et de l’interface web |  |
| Utilisation – ouverture de la ressource | Oui | Oui | [Ouverture depuis l’interface web](manage-assets.md#previewing-assets) ou de l’outil de recherche |
| Utilisation : placer une ressource de la gestion des actifs numériques dans un document | Oui – incorporation | Oui – liaison ou incorporation | [!DNL Experience Manager]L’application de bureau donne accès aux ressources sous forme de fichiers sur le système de fichiers local. Ces liens dans les applications natives sont représentés par des chemins d’accès locaux. |
| Modification – ouvrir pour modification | Oui – action d’extraction | Oui – action d’ouverture (dans le partage réseau) | L’[extraction dans AAL](https://helpx.adobe.com/fr/enterprise/using/manage-assets-using-adobe-asset-link.html) enregistre la ressource dans le compte de stockage Creative Cloud de l’utilisateur (synchronisé par l’application Creative Cloud) par défaut. |
| Modifier : travail en cours en dehors de DAM | Oui – ressource disponible dans le compte de stockage Creative Cloud de l’utilisateur synchronisé avec le poste de travail. | Oui |  |
| Modification – téléchargement des modifications | Oui – [Action d’archivage](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) avec des commentaires facultatifs | Oui |  |
| Téléchargement – fichier unique | Oui – téléchargement du document actif | Oui | [Chargement via l’interface web](manage-assets.md#uploading-assets) |
| Téléchargement – plusieurs fichiers/structures de dossiers hiérarchiques | Non | Oui | [Chargement via l’interface web](manage-assets.md#uploading-assets) ou par le biais d’un script ou d’un outil personnalisé. |
| Divers – utilisateur et connexion | L’utilisateur Creative Cloud connecté à l’application de bureau Creative Cloud est reconnu (SSO) | [!DNL Experience Manager] utilisateur et informations d’identification | Les utilisateurs des deux solutions sont comptabilisés dans la variable [!DNL Experience Manager] quota d’utilisateurs. |
| Divers – réseau et accès | Nécessite un accès depuis le bureau de l’utilisateur à [!DNL Experience Manager] déploiement sur réseau | Nécessite un accès depuis le bureau de l’utilisateur à [!DNL Experience Manager] déploiement sur réseau | [!DNL Adobe Asset Link] ne partage pas l’environnement proxy réseau. |
| Divers - migration d’un grand nombre de ressources | Non | Non | [Guide de migration des ressources](assets-migration-guide.md) |

Pour prendre en charge les cas d’utilisation de la distribution des ressources, d’autres solutions doivent être envisagées :

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) pour un module complémentaire SaaS configurable à [!DNL Experience Manager Assets] pour publier des ressources.
* Les solutions personnalisées sont créées à partir de la base de code [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager][Partage de liens](/help/assets/link-sharing.md) pour partager des ressources ad hoc à l’aide de liens.
* [Interface web de Experience Manager Assets](/help/assets/manage-assets.md) avec des zones sécurisées par les parties externes [!DNL Experience Manager] configuration du contrôle d’accès et avec les ajustements nécessaires de la configuration informatique/réseau, permettant à ces utilisateurs externes d’accéder à [!DNL Experience Manager].

## Concepts clés et cas d’utilisation {#key-concepts-and-use-cases}

### Glossaire des termes courants {#glossary-of-common-terms}

* **Travail en cours ou travail créatif en cours (WIP) :** phase dans le cycle de vie des ressources où une ressource est soumise à de multiples modifications et n’est généralement pas encore prête à être partagée avec les équipes élargies.
* **Ressources prêtes pour les créatifs :** [!DNL Assets] qui sont prêts à être partagés avec une équipe plus large ou qui ont été sélectionnés ou approuvés par l’équipe créative pour le partage avec les équipes marketing ou métier.
* **Approbation des ressources :** processus d’approbation traitant des ressources déjà transférées dans la gestion des ressources numériques (DAM), qui inclut généralement les approbations de marque, les validations juridiques, etc.
* **Ressource finale :** ressource qui a passé l’ensemble des approbations/balisages de métadonnées et qui est prête à être utilisée par l’équipe élargie. Une telle ressource est stockée dans la gestion des ressources numériques (DAM) et est accessible à tous les utilisateurs (ou à tous les utilisateurs intéressés). Il peut être utilisé dans les canaux marketing ou par des équipes créatives pour créer des conceptions.
* **Mise à jour/modification mineure des ressources :** modification rapide et petite d’une ressource numérique. Cette opération est souvent effectuée en réponse à une demande de retouche ou de modification mineure, de révision ou d’approbation de fichier (par exemple, repositionnement, modification de la taille du texte, ajustement de la saturation/luminosité, couleur, etc.).
* **Mise à jour/modification majeure des ressources :** modification d’une ressource numérique qui nécessite un travail considérable et qui doit parfois être effectuée sur une plus longue période de temps. Celle-ci implique généralement plusieurs modifications. La ressource doit être enregistrée plusieurs fois lors de la mise à jour. En règle générale, les mises à jour majeures de la ressource entraînent le passage à une étape en cours.
* **DAM :** gestion des ressources numériques (en anglais, Digital Asset Management). Dans ce document, il est synonyme de [!DNL Experience Manager Assets], sauf mention contraire spécifique.
* **Utilisateur créatif :** professionnel de la création, qui crée des ressources numériques à l’aide des applications et services Creative Cloud. Dans certains cas, un utilisateur créatif peut faire partie d’une équipe créative qui peut utiliser Creative Cloud, mais ne crée pas de ressources numériques (comme un directeur créatif ou un chef d’équipe créative).
* **Utilisateur de la gestion des ressources numériques :** utilisateur ordinaire d’un système de gestion des ressources numériques (DAM, Digital Asset Management). Selon l’organisation, l’utilisateur de gestion des ressources numériques (DAM) peut être un utilisateur marketing ou non, par exemple, un utilisateur métier, un bibliothécaire, un commercial, etc.

### Remarques concernant l’utilisation de [!DNL Experience Manager] et [!DNL Creative Cloud] integration {#considerations-when-using-aem-and-creative-cloud-integration}

* Voir [Bonnes pratiques relatives aux applications de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* Voir [Intégration d’Adobe Stock](aem-assets-adobe-stock.md)
* Voir la section [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Voici un bref résumé des bonnes pratiques pour [!DNL Experience Manager] et [!DNL Creative Cloud] intégration. Lisez la suite de ce document pour obtenir une description détaillée des points suivants.

* **Pour les utilisateurs créatifs qui travaillent dans Photoshop, InDesign ou Illustrator :** Adobe Asset Link offre la meilleure expérience utilisateur, y compris une gestion propre du travail en cours sur les ressources extraites à partir de [!DNL Experience Manager].
* **Pour simplifier l’accès aux ressources du bureau pour tout format de fichier ou application générique :** use [!DNL Experience Manager] application de bureau .
* **Comprendre pourquoi et quand stocker des ressources dans la gestion des ressources numériques :** Mises à jour à mettre à la disposition de l’équipe élargie de votre entreprise.
* **Tenez compte du volume des ressources partagées :** si votre cas d’utilisation est la distribution des ressources, la gouvernance et la sécurité peuvent être les aspects les plus importants. Envisagez d’utiliser des outils conçus pour effectuer les tâches à grande échelle, comme Brand Portal.
* **Comprendre le cycle de vie des ressources :** comprenez la façon dont les ressources sont traitées par les différentes équipes au sein de votre organisation.
* **Gérer avec soin les enregistrements fréquents des ressources :** Adobe Asset Link s’en charge à votre place avec PS, IA, ID. Pour d’autres applications, ne conservez pas de tâches en cours dans le dossier mappé/partagé, sauf si vous avez besoin de toutes les modifications dans DAM.

### Accès à [!DNL Adobe Stock] ressources à partir de [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[Intégration de Experience Manager et Adobe Stock](/help/assets/aem-assets-adobe-stock.md) fournit [!DNL Experience Manager] les utilisateurs qui peuvent rechercher, prévisualiser, acquérir sous licence et enregistrer des ressources provenant de [!DNL Adobe Stock] into [!DNL Experience Manager]. Sous licence et enregistré [!DNL Stock] ressources sélectionnées [!DNL Stock] métadonnées qui peuvent être utilisées pour les rechercher avec des filtres supplémentaires.

Quelques points importants à savoir concernant cette intégration :

* Lorsque les ressources du stock d’Adobe sont enregistrées dans [!DNL Experience Manager], ils deviennent des [!DNL Assets], avec un fichier binaire enregistré dans la variable [!DNL Experience Manager] référentiel. Certaines métadonnées liées à [!DNL Adobe Stock] sont enregistrés pour la ressource dans [!DNL Experience Manager], sinon le processus d’ingestion ressemble à celui de tout autre fichier. Par exemple, si les balises dynamiques sont actives, les balises sont ajoutées à ces fichiers lors de l’enregistrement.
* La ressource enregistrée dans [!DNL Experience Manager] est une copie et non un lien vers [!DNL Adobe Stock].

**Utilisation de ressources enregistrées à partir de [!DNL Adobe Stock] into [!DNL Experience Manager] in[!DNL Creative Cloud]**. Cette intégration est indépendante de [!DNL Adobe Asset Link], mais [!DNL Adobe Asset Link] reconnaît ces ressources enregistrées depuis [!DNL Stock] de cette manière, et affiche des métadonnées supplémentaires et un [!DNL Adobe Stock] logo sur ces ressources dans [!DNL Adobe Asset Link] l’interface utilisateur d’extension dans [!DNL Photoshop], [!DNL Illustrator]ou [!DNL InDesign]. Les fichiers peuvent être parcourus, ouverts, etc., car il s’agit de ressources standard lorsqu’ils sont enregistrés dans [!DNL Experience Manager].
Utilisateurs créatifs travaillant dans [!DNL Creative Cloud] applications avec [!DNL Adobe Asset Link] présente, en plus d’avoir accès aux ressources déjà sous licence à partir de [!DNL Adobe Stock] into [!DNL Experience Manager], peut également utiliser [!DNL Creative Cloud] Panneau Bibliothèques pour rechercher, prévisualiser et obtenir une licence [!DNL Adobe Stock] ressources.
[!DNL Assets] de [!DNL Adobe Stock] sous licence et enregistrés [!DNL Experience Manager] sont accessibles aux équipes élargies qui y accèdent ; [!DNL Experience Manager Assets] déploiement, tandis que les créatifs accordent une licence aux ressources à partir de [!DNL Adobe Stock] via [!DNL Creative Cloud] Le panneau Bibliothèques les rend disponibles uniquement par défaut dans leur [!DNL Creative Cloud] compte .

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## À propos du stockage de ressources dans un système de gestion des ressources numériques (DAM)  {#about-storing-assets-in-a-dam}

Pour établir un workflow efficace entre les équipes créatives et marketing/métier, et sélectionner les meilleures fonctionnalités de prise en charge, il est important de comprendre quand et pourquoi les ressources sont stockées dans la gestion des ressources numériques (DAM).

### Pourquoi les ressources sont-elles stockées dans la gestion des ressources numériques (DAM) ? {#why-assets-are-stored-in-dam}

Le stockage des ressources dans la gestion des ressources numériques (DAM) permet d’en faciliter l’accès et de les retrouver plus aisément. Cela garantit que les ressources peuvent être exploitées par de nombreux utilisateurs au sein de votre organisation ou écosystème, qui comprend les partenaires, les clients, etc.

La plupart des organisations choisissent de stocker uniquement les ressources pertinentes pour les processus marketing/LOB en aval (publication sur des canaux tels que le canal web via [!DNL Experience Manager Sites] ou d’autres canaux diffusés par Adobe Experience Cloud (par Marketing Cloud, Advertising Cloud et mesurés par Analytics Cloud, à l’intention des utilisateurs/partenaires, etc.). En outre, les entreprises stockent les ressources qui peuvent être soumises à un processus de révision/approbation dans la gestion des ressources numériques (DAM). De cette manière, la gestion des ressources numériques (DAM) stocke principalement les ressources ayant de grandes chances d’être exploitées, en évitant de stocker les ressources inactives.

Le stockage des ressources est soumis à des considérations techniques et d’utilisation des ressources. La gestion des ressources numériques (DAM) fournit des services supplémentaires pour les ressources stockées, notamment l’extraction de métadonnées, le contrôle de version, la génération d’aperçus/de transcodage, la gestion des références et l’ajout d’informations de contrôle d’accès. Ces services utilisent davantage de temps et de ressources de votre infrastructure.

Souvent, le stockage de toutes les ressources et mises à jour n’est pas souhaitable. Par exemple, si les mises à jour de ressources spécifiques sont de mauvaise qualité et utilisent les ressources en excès, les ressources peuvent être stockées dans la gestion des ressources numériques (DAM).

#### Quand les ressources sont-elles stockées dans la gestion des ressources numériques (DAM) ? {#when-assets-are-stored-in-dam}

Les équipes créatives (et les organisations) ne sont généralement pas intéressées par le stockage des ressources à chaque étape de leur cycle de vie. Par exemple, elles évitent de stocker des ressources dans les cas suivants :

* Si les ressources doivent être finalisées ou sont soumises à expérimentation.
* Si les ressources ne passent pas le cycle de révision de l’équipe interne/créative.
* L’équipe dispose de ressources plus pertinentes que celle en question pour présenter son travail à des équipes externes.

En règle générale, les classes de ressources suivantes sont stockées dans la gestion des ressources numériques (DAM) :

* Les ressources ayant atteint une certaine maturité et que l’on estime prêtes à être partagées.
* Les ressources qui ont été présélectionnées par l’équipe créative.
* Les formats de ressources spécifiques qui sont utilisables ou demandés par le marketing, selon un contrat ou un accord spécifique (par exemple, des fichiers JPG convertis à partir de fichiers RAW, des TIFF/images à partir d’originaux PSD).

#### Quand les mises à jour de ressources sont-elles stockées dans la gestion des ressources numériques (DAM) ? {#when-updates-to-assets-are-stored-in-dam}

En règle générale, seules les mises à jour des ressources pertinentes pour un large ensemble d’utilisateurs de la gestion des ressources numériques doivent être stockées dans la gestion des ressources numériques (DAM). Cela garantit que les utilisateurs (marketing et fonctions similaires) voient uniquement les versions appropriées dans la chronologie des ressources de la gestion des ressources numériques (DAM).

Généralement, il s’agit des modifications en rapport avec les principaux jalons dans le cycle de vie des ressources. Par exemple, la ressource initiale prête pour les spécialistes marketing ou une mise à jour officielle basée sur une demande/révision fournie par l’équipe créative doit être enregistrée et versionnée dans la gestion des ressources numériques (DAM).

Il peut s’agir, par exemple, d’une mise à jour de l’équipe créative pour révision par l’équipe marketing après une demande de modification de la ressource existante dans la gestion des ressources numériques (DAM). Elle doit être stockée et versionnée dans la gestion des ressources numériques (DAM) à des fins de référence ou pour revenir à la version précédente.

Voici quelques exemples de mises à jour qui ne sont généralement pas pertinentes :

* Les premières versions des ressources transférées avant qu’elles ne soient prêtes pour révision par le marketing
* Les modifications fréquentes de la ressource par l’équipe créative pendant la phase de travail en cours et avant que l’équipe créative ne décide que la ressource est prête

### Accès des utilisateurs à la gestion des ressources numériques (DAM)  {#user-access-to-dam}

[!DNL Assets] prend en charge deux types d’utilisateurs en fonction de leur accès au [!DNL Assets] déploiement. En règle générale, les utilisateurs à l’intérieur du réseau d’entreprise (pare-feu) ont un accès direct à la gestion des ressources numériques (DAM). Les autres utilisateurs à l’extérieur du réseau d’entreprise n’auront pas d’accès direct. Le type d’utilisateur détermine les intégrations qui peuvent être utilisées du point de vue technique.

#### Utilisateurs créatifs avec un accès direct à la gestion des ressources numériques (DAM) {#creative-users-with-direct-access-to-dam}

En règle générale, les équipes créatives internes ou les agences/créatifs professionnels intégrés au réseau interne ont accès au déploiement de la gestion des ressources numériques, y compris [!DNL Experience Manager] connectez-vous. [!DNL Experience Manager] et une infrastructure réseau peut être mise en place pour permettre un accès direct à des tiers externes (généralement des organisations de confiance telles que des agences travaillant pour un client), afin d’avoir accès à [!DNL Experience Manager] sur le réseau, par exemple via un VPN ou une liste autorisée IP.

Dans ce cas, Adobe d’un lien de ressource ou [!DNL Experience Manager] L’appli de bureau permet d’accéder facilement aux ressources finales/approuvées et d’enregistrer les ressources prêtes pour les créatifs dans la gestion des ressources numériques.

#### Utilisateurs créatifs sans accès à la gestion des ressources numériques (DAM)  {#creative-users-without-access-to-dam}

Les agences externes et les indépendants sans accès direct au déploiement de la gestion des ressources numériques peuvent avoir besoin d’un accès aux ressources approuvées ou souhaitent ajouter leurs nouvelles conceptions à la gestion des ressources numériques.

Utilisez les stratégies suivantes pour fournir un accès aux ressources finales/approuvées :

* Utilisez l’application de bureau si Asset Link ne fonctionne pas.
* Utilisez [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) pour distribuer les ressources en toute sécurité aux partenaires externes.
* Utilisez une implémentation personnalisée d’un portail de distribution et de source basé sur [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilisez la configuration du contrôle d’accès dans [!DNL Experience Manager] et l’infrastructure réseau nécessaire (par exemple, VPN et liste autorisée IP) pour permettre aux tiers externes d’accéder à une zone de contenu dédiée dans la gestion des ressources numériques. Ils peuvent utiliser [!DNL Experience Manager] Interface utilisateur web pour obtenir des ressources et charger du nouveau contenu dans la gestion des ressources numériques.

#### Travail en cours sur les ressources de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Comme indiqué dans ce document, il est recommandé d’effectuer des mises à jour majeures sur les ressources, parfois appelées travaux en cours, sans que toutes les modifications enregistrées dans le fichier local soient également chargées dans . [!DNL Experience Manager] comme modifications. Cela accélère le travail d’un utilisateur sur poste de travail, limite la bande passante réseau utilisée et maintient le calendrier des ressources ciblé sur les mises à jour majeures et contrôlées.

Adobe Asset Link est adapté à cas d’utilisation :

* Lorsque les utilisateurs [!DNL Photoshop], [!DNL InDesign]ou [!DNL Illustrator] dans le but de modifier un fichier, ils exécutent une opération d’extraction sur la ressource donnée.
* La ressource est téléchargée en arrière-plan, placée dans le compte de Creative Cloud des utilisateurs synchronisé sur le disque par l’appli de bureau Creative Cloud et l’indicateur d’extraction est activé/désactivé. [!DNL Experience Manager] sur la ressource pour minimiser les conflits de modification
* À ce stade, l’utilisateur utilise un fichier stocké localement dans l’emplacement synchronisé et peut continuer à travailler et à enregistrer les modifications nécessaires selon la fréquence nécessaire.
* De plus, comme la ressource figure dans le compte Creative Cloud, elle est également disponible sur d’autres appareils appartenant à l’utilisateur (par exemple, elle peut être ouverte ou modifiée dans une application mobile Creative Cloud dédiée) et peut être partagée avec d’autres utilisateurs Creative Cloud à des fins de collaboration.
* Lorsque l’utilisateur créatif a terminé d’apporter des modifications, il peut effectuer une opération d’archivage sur ce fichier dans son application Creative Cloud, en fournissant un commentaire facultatif. La ressource correspondante dans [!DNL Experience Manager] sont versionnés et mis à jour vers avec le nouveau fichier binaire. [!DNL Experience Manager] Les utilisateurs tels que les marketeurs ou les utilisateurs de la plate-forme métier ont accès aux modifications majeures de ressources, ou jalons, via [!DNL Experience Manager] interface utilisateur de la chronologie des ressources.

[!DNL Experience Manager]L’application de bureau propose un partage réseau pour les ressources ouvertes dans l’application native. Par défaut, toutes les modifications apportées localement sont téléchargées vers [!DNL Experience Manager] automatiquement après un bref moment. Avec une telle configuration, les enregistrements fréquents pendant la phase de travail en cours seront tous transférés dans [!DNL Experience Manager] et versionnés, créant un trafic réseau important et des défis potentiels d’évolutivité, sans parler des versions inutiles dans [!DNL Experience Manager].

L’approche recommandée ici consiste à utiliser une option dans [!DNL Experience Manager] Application de bureau pour désactiver les mises à jour automatisées et charger les modifications dans les ressources [!DNL Experience Manager] manuellement, en exploitant l’action de chargement des modifications dans l’interface utilisateur Asset Status de l’application.

#### Chargement en masse dans DAM {#bulk-upload-to-dam}

Dans certains cas, il est possible que vous deviez charger simultanément un plus grand nombre de fichiers dans la gestion des ressources numériques (DAM), par exemple :

* Chargement des résultats de séances photo ou projets de plus grande envergure
* Chargement de ressources fournies par les agences de création
* Transfert de ressources sélectionnées à partir d’un plus grand ensemble si la sélection est effectuée en dehors de la gestion des ressources numériques (DAM)

La description fait référence aux chargements de fichiers sur le plan opérationnel (par exemple, chaque semaine ou chaque séance photo), comme partie normale du processus de l’utilisateur de bureau. Les migrations de ressources de grande taille ne sont pas abordées ici.

Vous pouvez utiliser les fonctionnalités de transfert suivantes :

* Pour charger des dossiers hiérarchiques/volumineux en bloc, utilisez [!DNL Experience Manager] application de bureau qui fournit [téléchargement de dossier](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#upload-and-add-new-assets-to-aem) . Vous pouvez également transférer des structures de dossiers hiérarchiques. [!DNL Assets] sont chargées en arrière-plan et, par conséquent, elles ne sont pas liées à une session de navigateur web ;
* Pour charger quelques fichiers à partir d’un seul dossier, faites-les glisser directement vers l’interface web ou utilisez l’option Créer de la [!DNL Assets] interface web.
* En fonction des besoins de votre entreprise, vous pouvez également utiliser un outil de chargement personnalisé.

#### Gestion directe des ressources numériques depuis l’ordinateur de bureau {#managing-digital-assets-directly-from-desktop}

Si vous utilisez des partages de fichiers réseau pour gérer des ressources numériques, utilisez simplement le partage réseau mappé par [!DNL Experience Manager] L’appli de bureau peut être considérée comme un substitut pratique. Lors de la transition à partir de partages de fichiers réseau, [!DNL Experience Manager] L’interface web d’ offre un vaste ensemble de fonctionnalités de gestion des ressources numériques qui vont bien au-delà de ce qui est possible sur un partage réseau (recherche, collections, métadonnées, collaboration, aperçus, etc.), et [!DNL Experience Manager] L’appli de bureau fournit un lien pratique pour connecter le référentiel DAM côté serveur au travail sur le bureau.

Éviter d’utiliser [!DNL Experience Manager] de l’appli de bureau pour gérer les ressources directement dans le partage réseau de [!DNL Assets]. Par exemple, évitez d’utiliser [!DNL Experience Manager] L’appli de bureau pour déplacer/copier plusieurs fichiers. Utilisez plutôt la variable [!DNL Assets] pour faire glisser des dossiers du Finder/de l’Explorateur vers le partage réseau ou utiliser le [!DNL Assets] Fonction de chargement de dossier.

#### Migration de ressources {#asset-migration}

Pour planifier et exécuter des migrations de ressources depuis le système existant vers un nouveau système ou effectuer une migration d’un gros volumes de ressources stockées sur les serveurs, consultez le [Guide de migration](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] application de bureau et [!DNL Experience Manager] to [!DNL Creative Cloud] les intégrations ne prennent pas en charge ces migrations. En raison des grands volumes de ressources à assimiler et des exigences supplémentaires en termes de mappage, de transformation et d’intégration des métadonnées, les migrations doivent être gérées à l’aide d’outils et d’approches différents.

>[!MORELIKETHIS]
>
>* [Adobe d’un lien de ressource](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Bonnes pratiques relatives à l’appli de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=fr)
>* [Intégration d’Experience Manager et d’Adobe Stock](aem-assets-adobe-stock.md)

