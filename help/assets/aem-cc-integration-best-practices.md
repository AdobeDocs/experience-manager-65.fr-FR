---
title: Intégration aux bonnes pratiques de Adobe Creative Cloud
description: Bonnes pratiques pour intégrer  [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] afin de rationaliser les workflows de transfert de ressources et d’obtenir une vitesse de contenu élevée.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Collaboration,Adobe Asset Link,application de bureau
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
source-git-commit: c4cfb709162ca8f8f6e8508516c39542347c6bc4
workflow-type: tm+mt
source-wordcount: '3254'
ht-degree: 55%

---

# [!DNL Adobe Experience Manager] et bonnes pratiques  [!DNL Creative Cloud] d’intégration  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] est une solution de gestion des ressources numériques (DAM) qui peut s’intégrer  [!DNL Adobe Creative Cloud] à pour aider les utilisateurs de DAM à travailler avec des équipes créatives, en rationalisant la collaboration dans le processus de création de contenu.

[!DNL Adobe Creative Cloud] offre aux équipes créatives un écosystème de solutions et de services pour leur permettre de créer des ressources numériques. Il comprend des applications de bureau et mobiles, des services cloud tels que le stockage avec synchronisation de bureau ou expérience web, ainsi que des plateformes marketing telles que [!DNL Adobe Stock].

Lisez ce qui suit pour savoir quelles intégrations choisir entre poste de travail et DAM d’entreprise selon votre cas d’utilisation et découvrir quelles sont les bonnes pratiques associées aux workflows de connexion.

>[!NOTE]
>
>[!DNL Experience Manager] le partage de  [!DNL Creative Cloud] dossiers vers est obsolète et n’est plus traité dans ce guide. Adobe recommande d’utiliser des fonctionnalités plus récentes, telles que [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html) ou [l’appli de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html), pour permettre à l’utilisateur créatif d’accéder aux ressources gérées dans [!DNL Experience Manager].

## Besoins en matière de collaboration des créatifs, des marketeurs et des utilisateurs de la gestion des ressources numériques {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Conditions requises | Cas d’utilisation | Surfaces impliquées |
|---|---|---|
| Simplifier l’expérience pour les créatifs utilisant un poste de travail | Simplifiez l’accès aux ressources à partir d’une gestion des ressources numériques ([!DNL Experience Manager Assets]) pour les professionnels de la création ou, plus largement, pour les utilisateurs de bureau travaillant dans des applications de création de ressources natives. Ils ont besoin d’une méthode simple et simple pour découvrir, utiliser (ouvrir), modifier et enregistrer les modifications apportées à [!DNL Experience Manager], ainsi que charger de nouveaux fichiers. | Poste de travail Windows ou Mac ; [!DNL Creative Cloud] applications |
| Fournir des ressources de haute qualité et prêtes à l’emploi à partir de [!DNL Adobe Stock] | Les spécialistes marketing accélèrent le processus de création de contenu en contribuant à la recherche et à la découverte de ressources. Les créatifs utilisent les ressources approuvées directement dans leurs outils de création. | [!DNL Experience Manager Assets];  [!DNL Adobe Stock] le marché; Champs de métadonnées |
| Distribution et partage de ressources par sociétés | Les services internes/succursales locales et les partenaires externes, les distributeurs et les agences utilisent les ressources approuvées, partagées par la société mère. La société souhaite partager de manière sécurisée et transparente les ressources créées pour une réutilisation plus large. | Brand Portal, Asset Share Commons |

## Offres d’Adobe pour répondre aux besoins en matière de collaboration {#adobe-offerings-to-support-the-collaboration-need}

| Proposition de valeur pour les personnes impliquées | Offre d’Adobe | Surfaces impliquées |
|---|---|---|
| Les utilisateurs créatifs découvrent des ressources à partir de [!DNL Experience Manager], les ouvrent et les utilisent, modifient et chargent les modifications dans [!DNL Experience Manager], ainsi que chargent de nouveaux fichiers dans [!DNL Experience Manager], sans quitter les applications [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] et [!DNL Adobe InDesign]. |
| Les utilisateurs professionnels simplifient l’ouverture et l’utilisation des ressources, la modification et le chargement des modifications dans [!DNL Experience Manager] et le chargement de nouveaux fichiers dans [!DNL Experience Manager] à partir de l’environnement de bureau. Ils utilisent une intégration générique pour ouvrir n’importe quel type de ressource dans l’application de bureau native, y compris les applications autres qu’Adobe. | [Application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager]Application de bureau sous Windows et Mac |
| Les marketeurs et les utilisateurs professionnels découvrent, prévisualisent, attribuent une licence et enregistrent les ressources [!DNL Adobe Stock] et les gèrent depuis [!DNL Experience Manager]. Les ressources sous licence et enregistrées fournissent des [!DNL Adobe Stock] métadonnées sélectionnées pour une meilleure gouvernance. | [Intégration d’Experience Manager et d’Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interface web |

Cet article se concentre principalement sur les deux premiers aspects des besoins de collaboration. La distribution et la source des ressources à grande échelle sont brièvement mentionnées comme cas d’utilisation. Pour répondre à ces besoins, pensez à Adobe Brand Portal ou à Asset Share Commons. D’autres solutions telles que [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), des solutions qui peuvent être créées en fonction des [composants Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Partage de lien](/help/assets/link-sharing.md), à l’aide de [Ressources Experience Manager](/help/assets/manage-assets.md) doivent être examinées en fonction de besoins spécifiques.

![Connexions de Creative Cloud pour Experience Manager, choisissez la fonctionnalité à utiliser](assets/creative-connections-aem.png)

### Correspondance des cas d’utilisation aux solutions Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Exemple d’utilisation  | [!DNL Adobe Asset Link] | Appli de bureau [!DNL Experience Manager] | Remarques/autres solutions |
|---|---|---|---|
| Discover - parcourir les dossiers DAM | Oui | [!DNL Experience Manager] Actions de bureau et de l’interface web |  |
| Discover - Accès aux collections DAM | Oui | [!DNL Experience Manager] Actions de bureau et de l’interface web |  |
| Discover : recherche de ressources à partir de la gestion des ressources numériques | Oui | [!DNL Experience Manager] Actions de bureau et de l’interface web |  |
| Utilisation - ouverture de la ressource | Oui | Oui | [Ouverture depuis l’interface web](manage-assets.md#previewing-assets) ou de l’outil de recherche |
| Utilisation : placer une ressource de la gestion des actifs numériques dans un document | Oui - incorporation | Oui - liaison ou incorporation | [!DNL Experience Manager]L’application de bureau donne accès aux ressources sous forme de fichiers sur le système de fichiers local. Ces liens dans les applications natives sont représentés par des chemins d’accès locaux. |
| Modification - ouvrir pour modification | Oui - action d’extraction | Oui - action d’ouverture (dans le partage réseau) | L’[extraction dans AAL](https://helpx.adobe.com/fr/enterprise/using/manage-assets-using-adobe-asset-link.html) enregistre la ressource dans le compte de stockage Creative Cloud de l’utilisateur (synchronisé par l’application Creative Cloud) par défaut. |
| Modifier : travail en cours en dehors de DAM | Oui - ressource disponible dans le compte de stockage Creative Cloud de l’utilisateur synchronisé avec le poste de travail. | Oui |  |
| Modification - téléchargement des modifications | Oui - [Action d’archivage](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) avec des commentaires facultatifs | Oui |  |
| Téléchargement - fichier unique | Oui - téléchargement du document actif | Oui | [Chargement via l’interface web](manage-assets.md#uploading-assets) |
| Téléchargement - plusieurs fichiers/structures de dossiers hiérarchiques | Non | Oui | [Chargement via l’interface web](manage-assets.md#uploading-assets) ou par le biais d’un script ou d’un outil personnalisé. |
| Divers - utilisateur et connexion | L’utilisateur Creative Cloud connecté à l’application de bureau Creative Cloud est reconnu (SSO) | [!DNL Experience Manager] utilisateur et informations d’identification | Les utilisateurs des deux solutions sont pris en compte dans le quota d’utilisateurs [!DNL Experience Manager]. |
| Divers - réseau et accès | Nécessite un accès depuis le bureau de l’utilisateur au déploiement [!DNL Experience Manager] sur le réseau | Nécessite un accès depuis le bureau de l’utilisateur au déploiement [!DNL Experience Manager] sur le réseau | [!DNL Adobe Asset Link] ne partage pas l’environnement proxy réseau. |
| Divers - migration d’un grand nombre de ressources | Non | Non | [Guide de migration des ressources](assets-migration-guide.md) |

Pour prendre en charge les cas d’utilisation de la distribution des ressources, d’autres solutions doivent être envisagées :

* [Brand ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portal pour un module complémentaire SaaS configurable destiné  [!DNL Experience Manager Assets] à publier des ressources.
* Les solutions personnalisées sont créées à partir de la base de code [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager][Partage de liens](/help/assets/link-sharing.md) pour partager des ressources ad hoc à l’aide de liens.
* [L’](/help/assets/manage-assets.md) interface web de Experience Manager Assets avec des zones pour les parties externes sécurisées par la configuration du contrôle d’ [!DNL Experience Manager] accès et avec les réglages nécessaires de la configuration informatique/réseau, permettant à ces utilisateurs externes d’accéder à  [!DNL Experience Manager].

## Concepts clés et cas d’utilisation {#key-concepts-and-use-cases}

### Glossaire des termes courants {#glossary-of-common-terms}

* **Travail en cours ou travail créatif en cours (WIP) :** phase dans le cycle de vie des ressources où une ressource est soumise à de multiples modifications et n’est généralement pas encore prête à être partagée avec les équipes élargies.
* **Ressources prêtes pour les créations :** [!DNL Assets] prêtes à être partagées avec une équipe plus large, ou sélectionnées ou approuvées par l’équipe créative pour le partage avec les équipes marketing ou métier.
* **Approbation des ressources :** processus d’approbation traitant des ressources déjà transférées dans la gestion des ressources numériques, qui inclut généralement les approbations de marque, les validations juridiques, etc.
* **Ressource finale :** ressource qui a passé l’ensemble des approbations/balisages de métadonnées et qui est prête à être utilisée par l’équipe élargie. Une telle ressource est stockée dans la gestion des ressources numériques et est accessible à tous les utilisateurs (ou à tous les utilisateurs intéressés). Il peut être utilisé dans les canaux marketing ou par des équipes créatives pour créer des conceptions.
* **Mise à jour/modification mineure des ressources :** modification rapide et petite d’une ressource numérique. Cette opération est souvent effectuée en réponse à une demande de retouche ou de modification mineure, de révision ou d’approbation de fichier (par exemple, repositionnement, modification de la taille du texte, ajustement de la saturation/luminosité, couleur, etc.).
* **Mise à jour/modification majeure des ressources :** modification d’une ressource numérique qui nécessite un travail considérable et qui doit parfois être effectuée sur une plus longue période de temps. Celle-ci implique généralement plusieurs modifications. La ressource doit être enregistrée plusieurs fois lors de la mise à jour. En règle générale, les mises à jour majeures de la ressource entraînent le passage à une étape en cours.
* **DAM :** gestion des ressources numériques (en anglais, Digital Asset Management). Dans ce document, il est synonyme de [!DNL Experience Manager Assets], sauf mention contraire spécifique.
* **Utilisateur créatif :** professionnel de la création, qui crée des ressources numériques à l’aide des applications et services Creative Cloud. Dans certains cas, un utilisateur créatif peut faire partie d’une équipe créative qui peut utiliser Creative Cloud, mais ne crée pas de ressources numériques (comme un directeur créatif ou un chef d’équipe créative).
* **Utilisateur de la gestion des ressources numériques :** utilisateur ordinaire d’un système de gestion des ressources numériques (DAM, Digital Asset Management). Selon l’organisation, l’utilisateur de gestion des ressources numériques peut être un utilisateur marketing ou non, par exemple, un utilisateur métier, un bibliothécaire, un commercial, etc.

### Remarques concernant l’utilisation de l’intégration [!DNL Experience Manager] et [!DNL Creative Cloud] {#considerations-when-using-aem-and-creative-cloud-integration}

* Voir [Bonnes pratiques relatives à l’appli de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)
* Voir [Intégration Adobe Stock](aem-assets-adobe-stock.md)
* Voir la section [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Il s’agit d’un bref résumé des bonnes pratiques pour l’intégration de [!DNL Experience Manager] et [!DNL Creative Cloud]. Lisez la suite de ce document pour obtenir une description détaillée des points suivants.

* **Pour les utilisateurs créatifs travaillant dans Photoshop, InDesign ou Illustrator :** Adobe Asset Link offre la meilleure expérience utilisateur, y compris une gestion propre du travail en cours sur les ressources extraites à partir de  [!DNL Experience Manager].
* **Pour simplifier l’accès aux ressources du bureau pour tout format de fichier ou application générique :**  utilisez l’appli de  [!DNL Experience Manager] bureau .
* **Comprendre pourquoi et quand stocker des ressources dans la gestion des ressources numériques :**  mises à jour à mettre à la disposition de l’équipe élargie de votre entreprise.
* **Tenez compte du volume des ressources partagées :** si votre cas d’utilisation est la distribution des ressources, la gouvernance et la sécurité peuvent être les aspects les plus importants. Envisagez d’utiliser des outils conçus pour effectuer les tâches à grande échelle, comme Brand Portal.
* **Comprendre le cycle de vie des ressources :** comprenez la façon dont les ressources sont traitées par les différentes équipes au sein de votre organisation.
* **Gérer avec soin les enregistrements fréquents des ressources :** Adobe Asset Link s’en charge à votre place avec PS, IA, ID. Pour d’autres applications, ne conservez pas de tâches en cours dans le dossier mappé/partagé, sauf si vous avez besoin de toutes les modifications dans DAM.

### Accès aux [!DNL Adobe Stock] ressources à partir de [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[L’](/help/assets/aem-assets-adobe-stock.md) intégration de Experience Manager et Adobe Stock permet aux  [!DNL Experience Manager] utilisateurs de rechercher, de prévisualiser, d’acquérir sous licence et d’enregistrer des ressources  [!DNL Adobe Stock] dans  [!DNL Experience Manager]. Les ressources [!DNL Stock] sous licence et enregistrées ont sélectionné des métadonnées [!DNL Stock] qui peuvent être utilisées pour les rechercher avec des filtres supplémentaires.

Quelques points importants à savoir concernant cette intégration :

* Lorsque des ressources du stock d’Adobe sont enregistrées dans [!DNL Experience Manager], elles deviennent une balise [!DNL Assets] régulière, avec un fichier binaire enregistré dans le référentiel [!DNL Experience Manager]. Certaines métadonnées liées à [!DNL Adobe Stock] sont enregistrées pour la ressource dans [!DNL Experience Manager], sinon le processus d’ingestion ressemble à celui de tout autre fichier. Par exemple, si les balises dynamiques sont actives, les balises sont ajoutées à ces fichiers lors de l’enregistrement.
* La ressource enregistrée dans [!DNL Experience Manager] est une copie et non un lien vers [!DNL Adobe Stock].

**Utilisation de ressources enregistrées  [!DNL Adobe Stock] dans  [!DNL Experience Manager] dans[!DNL Creative Cloud]**. Cette intégration est indépendante de [!DNL Adobe Asset Link], mais [!DNL Adobe Asset Link] reconnaît ces ressources enregistrées à partir de [!DNL Stock] de cette façon et affiche des métadonnées supplémentaires et un logo [!DNL Adobe Stock] sur ces ressources dans l’interface utilisateur de l’extension [!DNL Adobe Asset Link] dans [!DNL Photoshop], [!DNL Illustrator] ou [!DNL InDesign]. Les fichiers peuvent être parcourus, ouverts, etc., car il s’agit de ressources normales lorsqu’ils sont enregistrés dans [!DNL Experience Manager].
Les utilisateurs créatifs qui travaillent dans des applications [!DNL Creative Cloud] avec une extension [!DNL Adobe Asset Link] présentes, en plus d’avoir accès à des ressources déjà sous licence de [!DNL Adobe Stock] vers [!DNL Experience Manager], peuvent également utiliser le panneau [!DNL Creative Cloud] Bibliothèques pour rechercher, prévisualiser et acquérir sous licence des ressources [!DNL Adobe Stock].
[!DNL Assets] des ressources  [!DNL Adobe Stock] sous licence et enregistrées dans  [!DNL Experience Manager] deviennent disponibles pour les équipes élargies accédant au  [!DNL Experience Manager Assets] déploiement, tandis que les équipes créatives octroyant des licences pour des ressources  [!DNL Adobe Stock] via le panneau  [!DNL Creative Cloud] Bibliothèques les rendent disponibles uniquement par défaut dans leur  [!DNL Creative Cloud] compte.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## À propos du stockage de ressources dans un système de gestion des ressources numériques {#about-storing-assets-in-a-dam}

Pour établir un workflow efficace entre les équipes créatives et marketing/métier, et sélectionner les meilleures fonctionnalités de prise en charge, il est important de comprendre quand et pourquoi les ressources sont stockées dans la gestion des ressources numériques (DAM).

### Pourquoi les ressources sont-elles stockées dans la gestion des ressources numériques ?  {#why-assets-are-stored-in-dam}

Le stockage des ressources dans la gestion des ressources numériques permet d’en faciliter l’accès et de les retrouver plus aisément. Cela garantit que les ressources peuvent être exploitées par de nombreux utilisateurs au sein de votre organisation ou écosystème, qui comprend les partenaires, les clients, etc.

La plupart des organisations choisissent de stocker uniquement les ressources pertinentes pour les processus marketing/LOB en aval (publication sur des canaux tels que le canal web via [!DNL Experience Manager Sites] ou d’autres canaux traités par Adobe Experience Cloud - Marketing Cloud, Advertising Cloud et mesurés par Analytics Cloud, satisfaction des besoins des utilisateurs/partenaires, etc.). En outre, les entreprises stockent les ressources qui peuvent être soumises à un processus de révision/approbation dans la gestion des ressources numériques. De cette manière, la gestion des ressources numériques stocke principalement les ressources ayant de grandes chances d’être exploitées, en évitant de stocker les ressources inactives.

Le stockage des ressources est soumis à des considérations techniques et d’utilisation des ressources. La gestion des ressources numériques fournit des services supplémentaires pour les ressources stockées, notamment l’extraction de métadonnées, le contrôle de version, la génération d’aperçus/de transcodage, la gestion des références et l’ajout d’informations de contrôle d’accès. Ces services utilisent davantage de temps et de ressources de votre infrastructure.

Souvent, le stockage de toutes les ressources et mises à jour n’est pas souhaitable. Par exemple, si les mises à jour de ressources spécifiques sont de mauvaise qualité et utilisent les ressources en excès, les ressources peuvent être stockées dans la gestion des ressources numériques.

#### Quand les ressources sont-elles stockées dans la gestion des ressources numériques ?  {#when-assets-are-stored-in-dam}

Les équipes créatives (et les organisations) ne sont généralement pas intéressées par le stockage des ressources à chaque étape de leur cycle de vie. Par exemple, elles évitent de stocker des ressources dans les cas suivants :

* Si les ressources doivent être finalisées ou sont soumises à expérimentation.
* Si les ressources ne passent pas le cycle de révision de l’équipe interne/créative.
* L’équipe dispose de ressources plus pertinentes que celle en question pour présenter son travail à des équipes externes.

En règle générale, les classes de ressources suivantes sont stockées dans la gestion des ressources numériques :

* Les ressources ayant atteint une certaine maturité et que l’on estime prêtes à être partagées.
* Les ressources qui ont été présélectionnées par l’équipe créative.
* Les formats de ressources spécifiques qui sont utilisables ou demandés par le marketing, selon un contrat ou un accord spécifique (par exemple, des fichiers JPG convertis à partir de fichiers RAW, des TIFF/images à partir d’originaux PSD).

#### Quand les mises à jour de ressources sont-elles stockées dans la gestion des ressources numériques ?  {#when-updates-to-assets-are-stored-in-dam}

En règle générale, seules les mises à jour des ressources pertinentes pour un large ensemble d’utilisateurs de la gestion des ressources numériques doivent être stockées dans la gestion des ressources numériques. Cela garantit que les utilisateurs (marketing et fonctions similaires) voient uniquement les versions appropriées dans la chronologie des ressources de la gestion des ressources numériques.

Généralement, il s’agit des modifications en rapport avec les principaux jalons dans le cycle de vie des ressources. Par exemple, la ressource initiale prête pour les spécialistes marketing ou une mise à jour officielle basée sur une demande/révision fournie par l’équipe créative doit être enregistrée et versionnée dans la gestion des ressources numériques.

Il peut s’agir, par exemple, d’une mise à jour de l’équipe créative pour révision par l’équipe marketing après une demande de modification de la ressource existante dans la gestion des ressources numériques. Elle doit être stockée et versionnée dans la gestion des ressources numériques à des fins de référence ou pour revenir à la version précédente.

Voici quelques exemples de mises à jour qui ne sont généralement pas pertinentes :

* Les premières versions des ressources transférées avant qu’elles ne soient prêtes pour révision par le marketing
* Les modifications fréquentes de la ressource par l’équipe créative pendant la phase de travail en cours et avant que l’équipe créative ne décide que la ressource est prête

### Accès des utilisateurs à la gestion des ressources numériques {#user-access-to-dam}

[!DNL Assets] prend en charge deux types d’utilisateurs en fonction de leur accès au  [!DNL Assets] déploiement. En règle générale, les utilisateurs à l’intérieur du réseau d’entreprise (pare-feu) ont un accès direct à la gestion des ressources numériques. Les autres utilisateurs à l’extérieur du réseau d’entreprise n’auront pas d’accès direct. Le type d’utilisateur détermine les intégrations qui peuvent être utilisées du point de vue technique.

#### Utilisateurs créatifs avec un accès direct à la gestion des ressources numériques  {#creative-users-with-direct-access-to-dam}

En règle générale, les équipes créatives internes ou les agences/professionnels de la création intégrés au réseau interne ont accès au déploiement de la gestion des ressources numériques, y compris la connexion [!DNL Experience Manager]. [!DNL Experience Manager] et une infrastructure réseau peut être mise en place pour permettre un accès direct à des tiers externes (généralement des organisations de confiance comme des agences travaillant pour un client), pour avoir accès à  [!DNL Experience Manager] via un réseau, par exemple par le biais d&#39;un VPN ou d&#39;une liste autorisée IP.

Dans ce cas, l’application de bureau Adobe Asset Link ou [!DNL Experience Manager] permet d’accéder facilement aux ressources finales/approuvées et d’enregistrer les ressources prêtes pour les créatifs dans la gestion des ressources numériques.

#### Utilisateurs créatifs sans accès à la gestion des ressources numériques {#creative-users-without-access-to-dam}

Les agences externes et les indépendants sans accès direct au déploiement de la gestion des ressources numériques peuvent avoir besoin d’un accès aux ressources approuvées ou souhaitent ajouter leurs nouvelles conceptions à la gestion des ressources numériques.

Utilisez les stratégies suivantes pour fournir un accès aux ressources finales/approuvées :

* Utilisez l’application de bureau si Asset Link ne fonctionne pas.
* Utilisez [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) pour distribuer les ressources en toute sécurité aux partenaires externes.
* Utilisez une implémentation personnalisée d’un portail de distribution et de source basé sur [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilisez la configuration du contrôle d’accès dans [!DNL Experience Manager] et l’infrastructure réseau nécessaire (par exemple, la liste autorisée VPN et IP) pour permettre aux tiers externes d’accéder à une zone de contenu dédiée dans la gestion des ressources numériques. Ils peuvent utiliser [!DNL Experience Manager] l’interface utilisateur web pour obtenir des ressources et charger du nouveau contenu dans la gestion des ressources numériques.

#### Travail en cours sur les ressources de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Comme indiqué dans ce document, il est recommandé d’effectuer des mises à jour majeures sur les ressources, parfois appelées travaux en cours, sans que toutes les modifications enregistrées dans le fichier local soient également chargées dans [!DNL Experience Manager] en tant que modifications. Cela accélère le travail d’un utilisateur sur poste de travail, limite la bande passante réseau utilisée et maintient le calendrier des ressources ciblé sur les mises à jour majeures et contrôlées.

Adobe Asset Link est adapté à cas d’utilisation :

* Lorsque les utilisateurs de [!DNL Photoshop], [!DNL InDesign] ou [!DNL Illustrator] ont l’intention de modifier un fichier, ils exécutent une opération d’extraction sur la ressource donnée.
* La ressource est téléchargée en arrière-plan, placée dans le compte de Creative Cloud des utilisateurs synchronisé sur le disque par l’appli de bureau Creative Cloud, et l’indicateur d’extraction est activé/désactivé dans [!DNL Experience Manager] sur la ressource afin de minimiser les conflits de modification.
* À ce stade, l’utilisateur utilise un fichier stocké localement dans l’emplacement synchronisé et peut continuer à travailler et à enregistrer les modifications nécessaires selon la fréquence nécessaire.
* De plus, comme la ressource figure dans le compte Creative Cloud, elle est également disponible sur d’autres appareils appartenant à l’utilisateur (par exemple, elle peut être ouverte ou modifiée dans une application mobile Creative Cloud dédiée) et peut être partagée avec d’autres utilisateurs Creative Cloud à des fins de collaboration.
* Lorsque l’utilisateur créatif a terminé d’apporter des modifications, il peut effectuer une opération d’archivage sur ce fichier dans son application Creative Cloud, en fournissant un commentaire facultatif. La ressource correspondante dans [!DNL Experience Manager] est versionnée et mise à jour vers avec le nouveau fichier binaire. [!DNL Experience Manager] Les utilisateurs tels que les marketeurs ou les utilisateurs de la plate-forme métier ont accès aux modifications majeures de ressources, ou jalons, via l’interface utilisateur de la chronologie des  [!DNL Experience Manager] ressources.

[!DNL Experience Manager]L’application de bureau propose un partage réseau pour les ressources ouvertes dans l’application native. Par défaut, toutes les modifications effectuées localement sont automatiquement chargées vers [!DNL Experience Manager] après un bref moment. Avec une telle configuration, les enregistrements fréquents pendant la phase de travail en cours seraient tous transférés dans [!DNL Experience Manager] et versionnés, ce qui créerait un grand nombre de trafic réseau et de défis d’évolutivité potentiels - sans parler des versions inutiles dans [!DNL Experience Manager].

L’approche recommandée ici consiste à utiliser une option dans l’appli de bureau [!DNL Experience Manager] pour désactiver les mises à jour automatisées et charger manuellement les modifications apportées aux ressources dans [!DNL Experience Manager], en exploitant l’action de chargement des modifications dans l’interface utilisateur État des ressources de l’application.

#### Chargement en masse dans DAM {#bulk-upload-to-dam}

Dans certains cas, il est possible que vous deviez charger simultanément un plus grand nombre de fichiers dans la gestion des ressources numériques, par exemple :

* Chargement des résultats de séances photo ou projets de plus grande envergure
* Chargement de ressources fournies par les agences de création
* Transfert de ressources sélectionnées à partir d’un plus grand ensemble si la sélection est effectuée en dehors de la gestion des ressources numériques

La description fait référence aux chargements de fichiers sur le plan opérationnel (par exemple, chaque semaine ou chaque séance photo), comme partie normale du processus de l’utilisateur de bureau. Les migrations de ressources de grande taille ne sont pas abordées ici.

Vous pouvez utiliser les fonctionnalités de transfert suivantes :

* Pour charger des dossiers hiérarchiques/volumineux en bloc, utilisez l’appli de bureau [!DNL Experience Manager] qui fournit la fonctionnalité [de chargement de dossiers](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem). Vous pouvez également transférer des structures de dossiers hiérarchiques. [!DNL Assets] sont chargées en arrière-plan et, par conséquent, elles ne sont pas liées à une session de navigateur web ;
* Pour charger quelques fichiers à partir d’un seul dossier, faites-les glisser directement vers l’interface web ou utilisez l’option Créer de l’interface web [!DNL Assets].
* En fonction des besoins de votre entreprise, vous pouvez également utiliser un outil de chargement personnalisé.

#### Gestion directe des ressources numériques à partir du bureau {#managing-digital-assets-directly-from-desktop}

Si vous utilisez des partages de fichiers réseau pour gérer des ressources numériques, le simple fait d’utiliser le partage réseau mappé par l’appli de bureau [!DNL Experience Manager] peut être considéré comme un substitut pratique. Lors de la transition à partir des partages de fichiers réseau, l’interface web [!DNL Experience Manager] fournit un vaste ensemble de fonctionnalités de gestion des ressources numériques qui vont bien au-delà de ce qui est possible sur un partage réseau (recherche, collections, métadonnées, collaboration, aperçus, etc.). L’appli de bureau [!DNL Experience Manager] fournit un lien pratique pour connecter le référentiel DAM côté serveur au travail sur le bureau.

Évitez d’utiliser l’appli de bureau [!DNL Experience Manager] pour gérer les ressources directement dans le partage réseau de [!DNL Assets]. Par exemple, évitez d’utiliser l’appli de bureau [!DNL Experience Manager] pour déplacer/copier plusieurs fichiers. Utilisez plutôt l’interface [!DNL Assets] pour faire glisser des dossiers du Finder/de l’Explorateur vers le partage réseau ou utilisez la fonction de téléchargement de dossiers [!DNL Assets].

#### Migration de ressources {#asset-migration}

Pour planifier et exécuter des migrations de ressources depuis le système existant vers un nouveau système ou effectuer une migration d’un gros volumes de ressources stockées sur les serveurs, consultez le [Guide de migration](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] L’appli de bureau et  [!DNL Experience Manager] les  [!DNL Creative Cloud] intégrations ne prennent pas en charge ces migrations. En raison des grands volumes de ressources à assimiler et des exigences supplémentaires en termes de mappage, de transformation et d’intégration des métadonnées, les migrations doivent être gérées à l’aide d’outils et d’approches différents.

>[!MORELIKETHIS]
>
>* [Adobe d’un lien de ressource](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Bonnes pratiques relatives à l’appli de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=fr)
>* [Intégration d’Experience Manager et d’Adobe Stock](aem-assets-adobe-stock.md)

