---
title: Intégration aux meilleures pratiques de Adobe Creative Cloud
description: Meilleures pratiques d'intégration [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] pour rationaliser les workflows de transfert d'actifs et atteindre une vitesse de contenu élevée.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
translation-type: tm+mt
source-git-commit: c4cfb709162ca8f8f6e8508516c39542347c6bc4
workflow-type: tm+mt
source-wordcount: '3254'
ht-degree: 55%

---

# [!DNL Adobe Experience Manager] et bonnes pratiques  [!DNL Creative Cloud] d’intégration  {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] est une solution de gestion des actifs numériques (DAM) qui peut s&#39;intégrer  [!DNL Adobe Creative Cloud] pour aider les utilisateurs de la gestion des actifs numériques à collaborer avec des équipes créatives, en rationalisant la collaboration dans le processus de création de contenu.

[!DNL Adobe Creative Cloud] offre aux équipes créatives un écosystème de solutions et de services pour leur permettre de créer des ressources numériques. Il comprend des applications de bureau et mobiles, des services cloud tels que l&#39;enregistrement avec synchronisation sur ordinateur de bureau ou l&#39;expérience Web, ainsi que des marchés tels que [!DNL Adobe Stock].

Lisez ce qui suit pour savoir quelles intégrations choisir entre poste de travail et DAM d’entreprise selon votre cas d’utilisation et découvrir quelles sont les bonnes pratiques associées aux workflows de connexion.

>[!NOTE]
>
>[!DNL Experience Manager] le partage de  [!DNL Creative Cloud] dossiers est obsolète et n’est plus couvert par ce guide. Adobe recommande d&#39;utiliser des fonctionnalités plus récentes, telles que [Adobe Asset Link](https://helpx.adobe.com/fr/enterprise/using/adobe-asset-link.html) ou [application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html), pour permettre à l&#39;utilisateur créatif d&#39;accéder aux ressources gérées dans [!DNL Experience Manager].

## Besoins de collaboration des créatifs, des marketeurs et des utilisateurs de DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Conditions requises | Cas d’utilisation | Surfaces impliquées |
|---|---|---|
| Simplifier l’expérience pour les créatifs utilisant un poste de travail | Simplifiez l&#39;accès aux ressources à partir d&#39;une gestion des actifs numériques ([!DNL Experience Manager Assets]) pour les professionnels de la création ou, plus généralement, pour les utilisateurs de bureau travaillant dans des applications de création d&#39;actifs natives. Ils ont besoin d&#39;une méthode simple et simple pour découvrir, utiliser (ouvrir), modifier et enregistrer les modifications dans [!DNL Experience Manager], ainsi que pour télécharger de nouveaux fichiers. | Ordinateur de bureau Windows ou Mac ; [!DNL Creative Cloud] applications |
| Fournir des ressources prêtes à l&#39;emploi de haute qualité à partir de [!DNL Adobe Stock] | Les spécialistes marketing accélèrent le processus de création de contenu en contribuant à la recherche et à la découverte de ressources. Les créatifs utilisent les ressources approuvées directement dans leurs outils de création. | [!DNL Experience Manager Assets];  [!DNL Adobe Stock] marché ; Champs de métadonnées |
| Distribution et partage de ressources par sociétés | Les services internes/succursales locales et les partenaires externes, les distributeurs et les agences utilisent les ressources approuvées, partagées par la société mère. La société souhaite partager de manière sécurisée et transparente les ressources créées pour une réutilisation plus large. | Brand Portal, Asset Share Commons |

## Offres d’Adobe pour répondre aux besoins en matière de collaboration {#adobe-offerings-to-support-the-collaboration-need}

| Proposition de valeur pour les personnes impliquées | Offre d’Adobe | Surfaces impliquées |
|---|---|---|
| Les utilisateurs créatifs découvrent des ressources de [!DNL Experience Manager], les ouvrent et les utilisent, modifient et téléchargent les modifications apportées à [!DNL Experience Manager] et téléchargent de nouveaux fichiers dans [!DNL Experience Manager], sans quitter les applications [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator] et [!DNL Adobe InDesign]. |
| Les utilisateurs professionnels simplifient l’ouverture et l’utilisation des ressources, la modification et le téléchargement des modifications dans [!DNL Experience Manager] et le téléchargement de nouveaux fichiers dans [!DNL Experience Manager] à partir de l’environnement de bureau. Ils utilisent une intégration générique pour ouvrir n’importe quel type de ressource dans l’application de bureau native, y compris les applications autres qu’Adobe. | [Application de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager]Application de bureau sous Windows et Mac |
| Les marketeurs et les utilisateurs professionnels découvrent, prévisualisation, concèdent des licences et enregistrent et gèrent les ressources [!DNL Adobe Stock] depuis [!DNL Experience Manager]. Les ressources sous licence et enregistrées fournissent des [!DNL Adobe Stock] métadonnées sélectionnées pour une meilleure gouvernance. | [Intégration d’Experience Manager et d’Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interface Web |

Cet article se concentre principalement sur les deux premiers aspects des besoins de collaboration. La distribution et la source des ressources à grande échelle sont brièvement mentionnées comme cas d’utilisation. Pour répondre à ces besoins, pensez à Adobe Brand Portal ou à Asset Share Commons. D’autres solutions, telles que [Portail de marque](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), qui peuvent être créées à partir des composants [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Link Share](/help/assets/link-sharing.md), à l’aide de [Experience Manager Assets](/help/assets/manage-assets.md), doivent être examinées en fonction de besoins spécifiques.

![Connexions Creative Cloud pour le Experience Manager, déterminer la capacité d’utiliser](assets/creative-connections-aem.png)

### Correspondance des cas d’utilisation aux solutions Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Exemple d’utilisation  | [!DNL Adobe Asset Link] | Appli de bureau [!DNL Experience Manager] | Remarques/autres solutions |
|---|---|---|---|
| Discover - parcourir les dossiers DAM | Oui | [!DNL Experience Manager] Interface Web et actions de bureau |  |
| Discover - Accès aux collections DAM | Oui | [!DNL Experience Manager] Interface Web et actions de bureau |  |
| Discover - Recherche de ressources à partir de DAM | Oui | [!DNL Experience Manager] Interface Web et actions de bureau |  |
| Utilisation - ouverture de la ressource | Oui | Oui | [Ouverture depuis l’interface web](manage-assets.md#previewing-assets) ou de l’outil de recherche |
| Utilisation : placer un fichier de la gestion des actifs numériques dans un document | Oui - incorporation | Oui - liaison ou incorporation | [!DNL Experience Manager]L’application de bureau donne accès aux ressources sous forme de fichiers sur le système de fichiers local. Ces liens dans les applications natives sont représentés par des chemins d’accès locaux. |
| Modification - ouvrir pour modification | Oui - action d’extraction | Oui - action d’ouverture (dans le partage réseau) | L’[extraction dans AAL](https://helpx.adobe.com/fr/enterprise/using/manage-assets-using-adobe-asset-link.html) enregistre la ressource dans le compte de stockage Creative Cloud de l’utilisateur (synchronisé par l’application Creative Cloud) par défaut. |
| Modifier : travail en cours en dehors de DAM | Oui - ressource disponible dans le compte de stockage Creative Cloud de l’utilisateur synchronisé avec le poste de travail. | Oui |  |
| Modification - téléchargement des modifications | Oui - [Action d’archivage](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) avec des commentaires facultatifs | Oui |  |
| Téléchargement - fichier unique | Oui - téléchargement du document actif | Oui | [Chargement via l’interface web](manage-assets.md#uploading-assets) |
| Téléchargement - plusieurs fichiers/structures de dossiers hiérarchiques | Non | Oui | [Chargement via l’interface web](manage-assets.md#uploading-assets) ou par le biais d’un script ou d’un outil personnalisé. |
| Divers - utilisateur et connexion | L’utilisateur Creative Cloud connecté à l’application de bureau Creative Cloud est reconnu (SSO) | [!DNL Experience Manager] informations d’identification et d’utilisateur | Les utilisateurs des deux solutions sont pris en compte dans le quota d’utilisateurs [!DNL Experience Manager]. |
| Divers - réseau et accès | Nécessite l&#39;accès du bureau de l&#39;utilisateur au déploiement [!DNL Experience Manager] sur le réseau | Nécessite l&#39;accès du bureau de l&#39;utilisateur au déploiement [!DNL Experience Manager] sur le réseau | [!DNL Adobe Asset Link] ne partage pas l&#39;environnement proxy réseau. |
| Divers - migration d’un grand nombre de ressources | Non | Non | [Guide de migration des ressources](assets-migration-guide.md) |

Pour prendre en charge les cas d’utilisation de la distribution des ressources, d’autres solutions doivent être envisagées :

* [Marque ](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) Portalpour un module complémentaire SaaS configurable permettant  [!DNL Experience Manager Assets] de publier des fichiers.
* Les solutions personnalisées sont créées à partir de la base de code [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager][Partage de liens](/help/assets/link-sharing.md) pour partager des ressources ad hoc à l’aide de liens.
* [Experience Manager Assets Web ](/help/assets/manage-assets.md) interfacte avec les zones pour les parties externes sécurisées par la configuration du  [!DNL Experience Manager] contrôle d&#39;accès et avec les ajustements nécessaires de configuration informatique/réseau, ce qui donne à ces utilisateurs externes accès à  [!DNL Experience Manager].

## Concepts clés et cas d’utilisation {#key-concepts-and-use-cases}

### Glossaire des termes courants {#glossary-of-common-terms}

* **Travail en cours ou travail créatif en cours (WIP) :** phase dans le cycle de vie des ressources où une ressource est soumise à de multiples modifications et n’est généralement pas encore prête à être partagée avec les équipes élargies.
* **Fichiers prêts pour la création :** [!DNL Assets] prêts à être partagés avec une équipe plus large, ou sélectionnés ou approuvés par l’équipe créative pour le partage avec les équipes marketing ou LOB.
* **Approbation des ressources :** processus d’approbation traitant des ressources déjà transférées dans la gestion des ressources numériques, qui inclut généralement les approbations de marque, les validations juridiques, etc.
* **Ressource finale :** ressource qui a passé l’ensemble des approbations/balisages de métadonnées et qui est prête à être utilisée par l’équipe élargie. Une telle ressource est stockée dans la gestion des ressources numériques et est accessible à tous les utilisateurs (ou à tous les utilisateurs intéressés). Il peut être utilisé dans les canaux marketing ou par des équipes créatives pour créer des conceptions.
* **Mise à jour/modification mineure des ressources :** modification rapide et petite d’une ressource numérique. Cette opération est souvent effectuée en réponse à une demande de retouche ou de modification mineure, de révision ou d’approbation de fichier (par exemple, repositionnement, modification de la taille du texte, ajustement de la saturation/luminosité, couleur, etc.).
* **Mise à jour/modification majeure des ressources :** modification d’une ressource numérique qui nécessite un travail considérable et qui doit parfois être effectuée sur une plus longue période de temps. Celle-ci implique généralement plusieurs modifications. La ressource doit être enregistrée plusieurs fois lors de la mise à jour. En règle générale, les mises à jour majeures de la ressource entraînent le passage à une étape en cours.
* **DAM :** gestion des ressources numériques (en anglais, Digital Asset Management). Dans ce document, il est synonyme de [!DNL Experience Manager Assets], sauf mention contraire.
* **Utilisateur créatif :** professionnel de la création, qui crée des ressources numériques à l’aide des applications et services Creative Cloud. Dans certains cas, un utilisateur créatif peut faire partie d’une équipe créative qui peut utiliser Creative Cloud, mais ne crée pas de ressources numériques (comme un directeur créatif ou un chef d’équipe créative).
* **Utilisateur de la gestion des ressources numériques :** utilisateur ordinaire d’un système de gestion des ressources numériques (DAM, Digital Asset Management). Selon l’organisation, l’utilisateur de gestion des ressources numériques peut être un utilisateur marketing ou non, par exemple, un utilisateur métier, un bibliothécaire, un commercial, etc.

### Considérations relatives à l’utilisation de l’intégration [!DNL Experience Manager] et [!DNL Creative Cloud] {#considerations-when-using-aem-and-creative-cloud-integration}

* Voir [meilleures pratiques relatives aux applications de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=en#best-practices-to-prevent-troubles)
* Voir [Intégration Adobe Stock](aem-assets-adobe-stock.md)
* Voir la section [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Il s&#39;agit d&#39;un bref résumé des meilleures pratiques pour l&#39;intégration [!DNL Experience Manager] et [!DNL Creative Cloud]. Lisez la suite de ce document pour obtenir une description détaillée des points suivants.

* **Pour les utilisateurs créatifs, qui travaillent dans Photoshop, InDesign ou Illustrator:** Adobe Asset Link offre la meilleure expérience d’utilisation, y compris la gestion correcte des travaux en cours sur les ressources extraites  [!DNL Experience Manager].
* **Pour simplifier l’accès aux ressources du bureau pour tout format de fichier générique ou toute application :** utilisez l’application  [!DNL Experience Manager] de bureau.
* **Comprenez pourquoi et quand stocker des ressources dans DAM :** Mises à jour à mettre à la disposition de l’équipe au sens large de votre organisation.
* **Tenez compte du volume des ressources partagées :** si votre cas d’utilisation est la distribution des ressources, la gouvernance et la sécurité peuvent être les aspects les plus importants. Envisagez d’utiliser des outils conçus pour effectuer les tâches à grande échelle, comme Brand Portal.
* **Comprendre le cycle de vie des ressources :** comprenez la façon dont les ressources sont traitées par les différentes équipes au sein de votre organisation.
* **Gérer avec soin les enregistrements fréquents des ressources :** Adobe Asset Link s’en charge à votre place avec PS, IA, ID. Pour d’autres applications, ne conservez pas de tâches en cours dans le dossier mappé/partagé, sauf si vous avez besoin de toutes les modifications dans DAM.

### Accès aux ressources [!DNL Adobe Stock] à partir de [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[L’](/help/assets/aem-assets-adobe-stock.md) intégration de Experience Manager et Adobe Stock permet aux  [!DNL Experience Manager] utilisateurs de rechercher, de prévisualisation, de licence et d’enregistrer des ressources  [!DNL Adobe Stock] dans  [!DNL Experience Manager]le. Les ressources [!DNL Stock] sous licence et enregistrées ont sélectionné des métadonnées [!DNL Stock] qui peuvent être utilisées pour les rechercher avec des filtres supplémentaires.

Quelques points importants à savoir concernant cette intégration :

* Lorsque des actifs du stock d&#39;Adobe sont enregistrés dans [!DNL Experience Manager], ils deviennent un [!DNL Assets] standard, avec un fichier binaire enregistré dans le référentiel [!DNL Experience Manager]. Certaines métadonnées relatives à [!DNL Adobe Stock] sont enregistrées pour la ressource dans [!DNL Experience Manager], sinon le processus d&#39;assimilation ressemble à tout autre fichier. Par exemple, si les balises dynamiques sont actives, les balises sont ajoutées à ces fichiers lors de l’enregistrement.
* La ressource enregistrée dans [!DNL Experience Manager] est une copie et non un lien de retour dans [!DNL Adobe Stock].

**Utilisation de ressources enregistrées  [!DNL Adobe Stock] dans  [!DNL Experience Manager][!DNL Creative Cloud]** dans. Cette intégration est indépendante de [!DNL Adobe Asset Link], mais [!DNL Adobe Asset Link] reconnaît ces actifs enregistrés à partir de [!DNL Stock] de cette façon et affiche des métadonnées supplémentaires et un logo [!DNL Adobe Stock] sur ces actifs dans l&#39;interface utilisateur de l&#39;extension [!DNL Adobe Asset Link] dans [!DNL Photoshop], [!DNL Illustrator] ou [!DNL InDesign]. Les fichiers peuvent être parcourus, ouverts, etc., car il s’agit de ressources normales lorsqu’ils sont enregistrés dans [!DNL Experience Manager].
Les utilisateurs créatifs travaillant dans des applications [!DNL Creative Cloud] dotées de l&#39;extension [!DNL Adobe Asset Link], en plus d&#39;avoir accès à des ressources déjà sous licence de [!DNL Adobe Stock] dans [!DNL Experience Manager], peuvent également utiliser le panneau [!DNL Creative Cloud] Bibliothèques pour rechercher, prévisualisation et accorder une licence à des ressources [!DNL Adobe Stock].
[!DNL Assets] sous  [!DNL Adobe Stock] licence et enregistrés dans  [!DNL Experience Manager] deviennent disponibles pour les équipes plus larges qui accèdent au  [!DNL Experience Manager Assets] déploiement, tandis que les créatifs qui octroient des licences à partir du panneau  [!DNL Adobe Stock] Bibliothèques les mettent à leur disposition uniquement par défaut dans leur  [!DNL Creative Cloud]   [!DNL Creative Cloud] compte.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## À propos du stockage de ressources dans un système de gestion des ressources numériques {#about-storing-assets-in-a-dam}

Pour établir un workflow efficace entre les équipes créatives et marketing/métier, et sélectionner les meilleures fonctionnalités de prise en charge, il est important de comprendre quand et pourquoi les ressources sont stockées dans la gestion des ressources numériques (DAM).

### Pourquoi les ressources sont-elles stockées dans la gestion des ressources numériques ?  {#why-assets-are-stored-in-dam}

Le stockage des ressources dans la gestion des ressources numériques permet d’en faciliter l’accès et de les retrouver plus aisément. Cela garantit que les ressources peuvent être exploitées par de nombreux utilisateurs au sein de votre organisation ou écosystème, qui comprend les partenaires, les clients, etc.

La plupart des entreprises choisissent de stocker uniquement les ressources pertinentes pour les processus marketing/LOB en aval (publication sur des canaux tels que le canal Web via [!DNL Experience Manager Sites] ou d’autres canaux fournis par Adobe Experience Cloud - Marketing Cloud, Advertising Cloud, et mesurés par Analytics Cloud, en fournissant aux utilisateurs/partenaires, etc.). En outre, les entreprises stockent les ressources qui peuvent être soumises à un processus de révision/approbation dans la gestion des ressources numériques. De cette manière, la gestion des ressources numériques stocke principalement les ressources ayant de grandes chances d’être exploitées, en évitant de stocker les ressources inactives.

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

En règle générale, les équipes de création interne, les agences et les professionnels de la création intégrés au réseau interne ont accès au déploiement de la gestion des actifs numériques, y compris à la [!DNL Experience Manager] connexion. [!DNL Experience Manager] et l&#39;infrastructure réseau peut être mise en place pour permettre l&#39;accès direct à des parties externes - généralement des organisations de confiance comme des agences travaillant pour un client - pour avoir accès à un réseau  [!DNL Experience Manager] via un réseau, par exemple via un VPN ou une liste autorisée IP.

Dans ce cas, l’application de bureau [!DNL Experience Manager] ou Adobe Asset Link permet d’accéder facilement aux ressources finales/approuvées et d’enregistrer des ressources prêtes à l’emploi dans la gestion des actifs numériques.

#### Utilisateurs créatifs sans accès à la gestion des ressources numériques {#creative-users-without-access-to-dam}

Les agences externes et les indépendants qui n&#39;ont pas accès directement au déploiement de la gestion des actifs numériques peuvent avoir besoin d&#39;accéder aux ressources approuvées ou d&#39;ajouter leurs nouvelles conceptions à la gestion des actifs numériques.

Utilisez les stratégies suivantes pour fournir un accès aux ressources finales/approuvées :

* Utilisez l’application de bureau si Asset Link ne fonctionne pas.
* Utiliser [Portail de marques des ressources Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) pour distribuer les ressources en toute sécurité à des partenaires externes
* Utilisez une implémentation personnalisée d’un portail de distribution et de source basé sur [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilisez le Contrôle d&#39;accès configuré dans [!DNL Experience Manager] et l&#39;infrastructure réseau nécessaire (par exemple, VPN et liste autorisée IP) pour permettre aux tiers externes d&#39;accéder à une zone de contenu dédiée dans votre DAM. Ils peuvent utiliser [!DNL Experience Manager] l&#39;interface utilisateur Web pour obtenir des ressources et télécharger du nouveau contenu dans votre gestion des actifs numériques.

#### Travaux en cours sur les actifs de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Comme nous l&#39;avons vu dans ce document, il est recommandé d&#39;effectuer des mises à jour majeures sur les ressources, parfois appelées travaux en cours, sans que toutes les modifications soient enregistrées dans le fichier local et téléchargées dans [!DNL Experience Manager] en tant que modifications. Cela accélère le travail d’un utilisateur sur poste de travail, limite la bande passante réseau utilisée et maintient le calendrier des ressources ciblé sur les mises à jour majeures et contrôlées.

Adobe Asset Link est adapté à cas d’utilisation :

* Lorsque les utilisateurs de [!DNL Photoshop], [!DNL InDesign] ou [!DNL Illustrator] ont l&#39;intention de modifier un fichier, ils exécutent une opération d&#39;extraction sur la ressource donnée.
* La ressource est téléchargée en arrière-plan, placée dans un compte utilisateur Creative Cloud synchronisé sur le disque par application de bureau Creative Cloud, et l&#39;indicateur de passage en caisse est basculé dans [!DNL Experience Manager] sur la ressource afin de minimiser les conflits de modification.
* À ce stade, l’utilisateur utilise un fichier stocké localement dans l’emplacement synchronisé et peut continuer à travailler et à enregistrer les modifications nécessaires selon la fréquence nécessaire.
* De plus, comme la ressource figure dans le compte Creative Cloud, elle est également disponible sur d’autres appareils appartenant à l’utilisateur (par exemple, elle peut être ouverte ou modifiée dans une application mobile Creative Cloud dédiée) et peut être partagée avec d’autres utilisateurs Creative Cloud à des fins de collaboration.
* Lorsque l’utilisateur créatif a terminé d’apporter des modifications, il peut effectuer une opération d’archivage sur ce fichier dans son application Creative Cloud, en fournissant un commentaire facultatif. Les ressources correspondantes dans [!DNL Experience Manager] sont versionnées et mises à jour avec le nouveau binaire. [!DNL Experience Manager] les utilisateurs tels que les marketeurs ou les utilisateurs de la liste d’attente ont accès à des modifications majeures de ressources, ou à des jalons, via l’interface utilisateur de la chronologie des  [!DNL Experience Manager] ressources.

[!DNL Experience Manager]L’application de bureau propose un partage réseau pour les ressources ouvertes dans l’application native. Par défaut, toutes les modifications effectuées localement sont automatiquement téléchargées vers [!DNL Experience Manager] après une brève période. Avec une telle configuration, les économies fréquentes pendant la phase de travail en cours seraient toutes téléchargées dans [!DNL Experience Manager] et versionnées, ce qui créerait beaucoup de trafic réseau et de défis potentiels d&#39;évolutivité - sans parler des versions inutiles dans [!DNL Experience Manager].

L’approche recommandée ici consiste à utiliser une option dans l’application de bureau [!DNL Experience Manager] pour désactiver les mises à jour automatisées et transférer manuellement les modifications apportées aux ressources vers [!DNL Experience Manager], en exploitant l’action de transfert des modifications dans l’interface utilisateur État des ressources de l’application.

#### Chargement en masse dans DAM {#bulk-upload-to-dam}

Dans certains cas, il est possible que vous deviez charger simultanément un plus grand nombre de fichiers dans la gestion des ressources numériques, par exemple :

* Chargement des résultats de photoshoots ou projets de plus grande envergure
* Chargement de ressources fournies par les agences de création
* Transfert de ressources sélectionnées à partir d’un plus grand ensemble si la sélection est effectuée en dehors de la gestion des ressources numériques

La description fait référence au téléchargement de fichiers de manière opérationnelle (par exemple, toutes les semaines ou avec chaque prise de vue), en tant que partie normale du processus de l’utilisateur de bureau. Les migrations de ressources de grande taille ne sont pas abordées ici.

Vous pouvez utiliser les fonctionnalités de transfert suivantes :

* Pour télécharger des dossiers volumineux/hiérarchiques en bloc, utilisez l’[!DNL Experience Manager] application de bureau qui offre la fonctionnalité de [téléchargement de dossiers](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#upload-and-add-new-assets-to-aem). Vous pouvez également transférer des structures de dossiers hiérarchiques. [!DNL Assets] sont téléchargés en arrière-plan et, par conséquent, ils ne sont pas liés à une session de navigateur Web.
* Pour télécharger quelques fichiers à partir d’un seul dossier, faites-les glisser directement vers l’interface Web ou utilisez l’option Créer de l’[!DNL Assets] interface Web.
* En fonction des besoins de votre entreprise, vous pouvez également utiliser un outil de chargement personnalisé.

#### Gérer les ressources numériques directement à partir du bureau {#managing-digital-assets-directly-from-desktop}

Si vous utilisez le partage de fichiers réseau pour gérer les ressources numériques, le simple fait d&#39;utiliser le partage réseau mappé par [!DNL Experience Manager] application de bureau peut être considéré comme un substitut pratique. Lors de la transition à partir de partages de fichiers réseau, [!DNL Experience Manager] l&#39;interface Web offre un ensemble riche de fonctionnalités de gestion des actifs numériques qui vont bien au-delà de ce qui est possible sur un partage réseau (recherche, collections, métadonnées, collaboration, prévisualisations, etc.). L&#39;application de bureau [!DNL Experience Manager] fournit un lien pratique permettant de connecter le référentiel DAM côté serveur au travail sur ordinateur.

Evitez d’utiliser l’[!DNL Experience Manager] application de bureau pour gérer directement les ressources dans le partage réseau de [!DNL Assets]. Par exemple, évitez d’utiliser l’application de bureau [!DNL Experience Manager] pour déplacer/copier plusieurs fichiers. Utilisez plutôt l&#39;interface [!DNL Assets] pour faire glisser des dossiers du Finder/Explorer vers le partage réseau ou utilisez la fonction de téléchargement de dossier [!DNL Assets].

#### Migration de ressources {#asset-migration}

Pour planifier et exécuter des migrations de ressources depuis le système existant vers un nouveau système ou effectuer une migration d’un gros volumes de ressources stockées sur les serveurs, consultez le [Guide de migration](/help/assets/assets-migration-guide.md). [!DNL Experience Manager] les applications de bureau et  [!DNL Experience Manager] les  [!DNL Creative Cloud] intégrations ne prennent pas en charge ces migrations. En raison des grands volumes de ressources à assimiler et des exigences supplémentaires en termes de mappage, de transformation et d’intégration des métadonnées, les migrations doivent être gérées à l’aide d’outils et d’approches différents.

>[!MORELIKETHIS]
>
>* [Lien de ressource Adobe](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [Meilleures pratiques pour les applications de bureau Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Portail des marques Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=fr)
>* [Intégration d’Experience Manager et d’Adobe Stock](aem-assets-adobe-stock.md)

