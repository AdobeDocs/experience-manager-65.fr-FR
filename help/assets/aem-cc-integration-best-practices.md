---
title: Meilleures pratiques d’intégration d’AEM et de Creative Cloud
description: Meilleures pratiques pour intégrer AEM à Adobe Creative Cloud afin de rationaliser les processus de transfert de ressources et d’optimiser l’efficacité.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# AEM and Creative Cloud integration best practices {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.4 article that's behind this article in terms of content streamlining and structuring.
-->

Adobe Experience Manager Assets est une solution de gestion des actifs numériques (DAM) qui peut s’intégrer à Adobe Creative Cloud pour aider les utilisateurs de DAM à travailler ensemble avec des équipes de création, en rationalisant la collaboration dans le processus de création de contenu.

Adobe Creative Cloud offre aux équipes créatives un écosystème de solutions et de services pour leur permettre de créer des ressources numériques. Il comprend des applications de bureau et mobiles, des services de cloud tels que le stockage avec une synchronisation sur poste de travail ou une expérience web, ainsi que des places de marché telles qu’Adobe Stock.

Lisez ce qui suit pour savoir quelles intégrations choisir entre poste de travail et DAM d’entreprise selon votre cas d’utilisation et découvrir quelles sont les meilleures pratiques associées aux workflows de connexion.

>[!NOTE]
>
>Le partage de dossiers AEM vers Creative Cloud est obsolète et n’est plus traité dans ce guide. Adobe recommends using newer capabilities such as [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) to provide creative user with access to assets managed in AEM.

## Collaboration needs of creatives, marketers, and DAM users {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Conditions requises | Cas d’utilisation   | Surfaces impliquées |
|---|---|---|
| Simplifier l’expérience pour les créatifs utilisant un poste de travail | Simplifiez l’accès aux ressources depuis DAM (AEM Assets) pour les créatifs ou, plus largement, pour les utilisateurs sur poste de travail utilisant des applications de création de ressources natives. Ils ont besoin d’une méthode simple et rapide pour découvrir, utiliser (ouvrir), modifier et enregistrer les modifications dans AEM, ainsi que pour télécharger de nouveaux fichiers. | Poste de travail Windows ou Mac ; applications Creative Cloud |
| Fournir des ressources de grande qualité, prêtes à l’emploi depuis Adobe Stock | Les marketeurs accélèrent le processus de création de contenu en contribuant à la recherche et à la découverte de ressources. Les créatifs utilisent les ressources approuvées directement dans leurs outils de création. | AEM Assets ; Adobe Stock Marketplace ; champs de métadonnées |
| Distribution et partage de ressources par sociétés | Les services internes/succursales locales et les partenaires externes, les distributeurs et les agences utilisent les ressources approuvées, partagées par la société mère. La société souhaite partager de manière sécurisée et transparente les ressources créées pour une réutilisation plus large. | Brand Portal, Asset Share Commons |

## Offres d’Adobe pour répondre aux besoins en matière de collaboration {#adobe-offerings-to-support-the-collaboration-need}

| Proposition de valeur pour les personnes impliquées | Offre d’Adobe | Surfaces impliquées |
|---|---|---|
| Les utilisateurs créatifs découvrent des ressources à partir d’AEM, les ouvrent et les utilisent, les modifient et téléchargent les modifications dans AEM et téléchargent aussi de nouveaux fichiers dans AEM sans quitter les applications Creative Cloud. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator et InDesign |
| Les utilisateurs professionnels simplifient l’ouverture et l’utilisation des ressources, la modification et le téléchargement des modifications dans AEM et le téléchargement de nouveaux fichiers dans AEM à partir de l’environnement de bureau. Ils utilisent une intégration générique pour ouvrir n’importe quel type de ressource dans l’application de bureau native, y compris les applications autres qu’Adobe. | [Application de bureau AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | Application de bureau AEM sous Windows et Mac |
| Les marketeurs et les utilisateurs professionnels découvrent, prévisualisent, attribuent une licence et enregistrent les ressources Adobe Stock dans AEM. Les ressources sous licence et enregistrées fournissent des métadonnées Adobe Stock pour une meilleure gouvernance. | [Intégration d’Experience Manager et d’Adobe Stock](aem-assets-adobe-stock.md) | Interface web d’AEM |

Cet article porte principalement sur les deux premiers aspects des besoins en matière de collaboration. La distribution et la source des ressources à l’échelle sont brièvement mentionnées comme cas d’utilisation. Pour ces besoins, envisagez d’utiliser Adobe Brand Portal ou Asset Share Commons. Alternate solutions such as [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html), solutions that can be built based on [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) components, [Link Share](/help/assets/link-sharing.md), using [Experience Manager Assets](/help/assets/managing-assets-touch-ui.md) should be reviewed based on specific requirement.

![Connexions Creative Cloud pour AEM : choix de la fonctionnalité à utiliser](assets/creative-connections-aem.png)

### Correspondance des cas d’utilisation aux solutions Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Exemple d’utilisation | Adobe Asset Link | Application de bureau AEM | Remarques/autres solutions |
|---|---|---|---|
| Découverte - parcours des dossiers AEM | Oui | Interface utilisateur web d’AEM + actions sur le poste de travail | Lors du parcours du partage réseau, désactivez les miniatures pour éviter de télécharger des fichiers binaires de ressources. |
| Découverte - accès aux collections AEM | Oui | Interface utilisateur web d’AEM + actions sur le poste de travail |  |
| Découverte - recherche de ressources à partir d’AEM | Oui | Interface utilisateur web d’AEM + actions sur le poste de travail |  |
| Utilisation - ouverture de la ressource | Oui | Oui - pour toutes les applications | [Ouvrir à partir de l&#39;interface](managing-assets-touch-ui.md#previewing-assets) Web ou du Finder |
| Utilisation - placement de la ressource d’AEM dans un document | Oui - incorporation | Oui - liaison ou incorporation | L’application de bureau AEM donne accès aux ressources sous forme de fichiers sur le système de fichiers local. Ces liens dans les applications natives sont représentés par des chemins d’accès locaux. |
| Modification - ouvrir pour modification | Oui - Action d’extraction | Oui - Action d’ouverture (dans le partage réseau) | [L’extraction dans AAL](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) enregistre la ressource dans le compte de stockage Creative Cloud de l’utilisateur (synchronisé par l’application Creative Cloud) par défaut. |
| Modification - tâche en cours en dehors d’AEM | Oui - Fichier disponible dans le compte de stockage Creative Cloud de l’utilisateur synchronisé sur le bureau. | Oui |  |
| Modification - téléchargement des modifications | Oui - [Action d’archivage](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) avec des commentaires facultatifs | Oui |  |
| Téléchargement - fichier unique | Oui - téléchargement du document actif | Oui | [Télécharger via l’interface Web](managing-assets-touch-ui.md#uploading-assets) |
| Téléchargement - plusieurs fichiers/structures de dossiers hiérarchiques | Non | Oui | [Télécharger via l’interface](managing-assets-touch-ui.md#uploading-assets)Web;<br>Script ou outil personnalisé |
| Divers - utilisateur et connexion | L’utilisateur Creative Cloud connecté à l’application de bureau Creative Cloud est reconnu (SSO) | Utilisateur/connexion AEM | Les utilisateurs des deux solutions sont comptabilisés par rapport au quota d’utilisateurs AEM. |
| Divers - réseau et accès | Nécessite un accès depuis le poste de travail de l’utilisateur vers le déploiement AEM sur le réseau | Nécessite un accès depuis le poste de travail de l’utilisateur vers le déploiement AEM sur le réseau | Adobe Asset Link ne partage pas l’environnement du proxy réseau. |
| Divers - migration d’un grand nombre de ressources | Non | Non | [Guide de migration](assets-migration-guide.md) |

Pour prendre en charge les cas d’utilisation de la distribution des ressources, d’autres solutions doivent être envisagées :

* [Portail](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) de marque pour un module complémentaire SaaS configurable aux ressources AEM pour publier des fichiers.
* Les solutions personnalisées sont créées à partir de la base de code [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [Partage de liens](/help/assets/link-sharing.md) AEM pour partager des ressources ad-hoc à l’aide de liens.
* [Interface web d’AEM Assets](/help/assets/managing-assets-touch-ui.md) avec des zones destinées aux parties externes, sécurisées par la configuration du contrôle d’accès AEM, et avec les ajustements de configuration informatique/réseau nécessaires pour permettre à ces utilisateurs externes d’accéder à AEM.

## Concepts clés et cas d’utilisation {#key-concepts-and-use-cases}

### Glossaire des termes courants {#glossary-of-common-terms}

* **Travail en cours ou travail créatif en cours (WIP) :** phase dans le cycle de vie des ressources où une ressource est soumise à de multiples modifications et n’est généralement pas encore prête à être partagée avec les équipes élargies.
* **** Ressources prêtes pour la création : Ressources prêtes à être partagées avec une équipe plus large ou sélectionnées/approuvées par l’équipe créative pour le partage avec les équipes marketing ou LOB.
* **Approbation des ressources :** processus d’approbation traitant des ressources déjà transférées dans la gestion des actifs numériques, qui inclut généralement les approbations de marque, les validations juridiques, etc.
* **Ressource finale :** ressource qui a passé toutes les   le balisage des approbations/métadonnées et est prêt à être utilisé par l’équipe élargie. Une telle ressource est stockée dans la gestion des actifs numériques et est accessible à tous les utilisateurs (ou à tous les utilisateurs intéressés). Elle peut être utilisée dans les canaux marketing ou par les équipes créatives de façon à créer des designs.
* **Mise à jour/modification mineure**  update/change : Changement rapide et léger d’une ressource numérique. Elle est souvent effectuée en réponse à une demande de modification mineure ou de retouche, à une révision de ressource ou à une approbation (par exemple, repositionnement, modification de la taille du texte, réglage de la luminosité/saturation, modification de la couleur, etc.).
* **Mise à jour/modification majeure**  update/change : Une modification d’une ressource numérique qui nécessite un travail considérable et qui doit parfois être effectuée sur une plus longue période de temps. De multiples modifications sont généralement impliquées. La ressource doit être enregistrée à plusieurs reprises au cours de la mise à jour. Les mises à jour majeures d’une ressource entraînent généralement le passage de la ressource à l’étape de travail en cours (WIP).
* **DAM :** gestion des actifs numériques (en anglais, Digital Asset Management). Dans ce document, il est synonyme d’Adobe Experience Manager (AEM) Assets, sauf mention contraire.
* **Utilisateur créatif :** professionnel de la création qui crée des ressources numériques avec les applications et services Creative Cloud. Dans certains cas, un utilisateur créatif peut être membre d’une équipe créative qui peut utiliser Creative Cloud sans toutefois créer de ressources numériques (comme un directeur artistique ou un responsable d’équipe créative).
* **** Utilisateur DAM : Utilisateur type d’un système de gestion des actifs numériques. Selon l’organisation, un utilisateur de gestion des actifs numériques peut être un utilisateur marketing ou non, par exemple, un utilisateur métier, un bibliothécaire, un commercial, etc.

### Remarques concernant l’utilisation d’AEM et de l’intégration Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

* See [desktop app best practices](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* Voir Intégration [d’Adobe Stock](aem-assets-adobe-stock.md)
* See [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Il s’agit d’un bref résumé des meilleures pratiques relatives à l’intégration d’Experience Manager et de Creative Cloud. Lisez la suite de ce document pour obtenir une description détaillée des points suivants.

* **Pour les utilisateurs créatifs, utilisant Photoshop, InDesign ou Illustrator :** Adobe Asset Link offre une expérience utilisateur optimale, notamment la gestion des tâches en cours sur les ressources extraites à partir d’AEM.
* **Pour simplifier l’accès aux ressources depuis un poste de travail pour une application ou un format de fichier générique :** utilisez l’application de bureau AEM.
* **Déterminer pourquoi et quand stocker des ressources dans la gestion des actifs numériques :** identifiez quelles mises à jour doivent être mises à la disposition de l’équipe élargie au sein de votre organisation.
* **Surveiller le volume des ressources partagées :** Si votre cas d’utilisation est la distribution des ressources, la gouvernance et la sécurité peuvent être les aspects les plus importants. Pensez à utiliser des outils conçus pour le faire à grande échelle, comme Brand Portal.
* **Comprendre le cycle de vie des ressources :** comprenez la façon dont les ressources sont traitées par les différentes équipes au sein de votre organisation.
* **Gérer avec soin les enregistrements fréquents des ressources :** Adobe Asset Link s’en charge à votre place avec PS, IA, ID. Pour d’autres applications, ne conservez pas de tâches en cours dans le dossier mappé/partagé, sauf si vous avez besoin de toutes les modifications dans DAM.

### Accès aux ressources Adobe Stock depuis AEM Assets {#access-to-adobe-stock-assets-from-aem-assets}

[L’intégration](/help/assets/aem-assets-adobe-stock.md) d’AEM et d’Adobe Stock permet aux utilisateurs d’AEM de rechercher, prévisualiser, activer et enregistrer des ressources d’Adobe Stock dans AEM. Les fichiers Adobe Stock sous licence et enregistrés ont sélectionné des métadonnées Stock, qui peuvent être utilisées pour les rechercher avec des filtres supplémentaires.

Quelques points importants à savoir concernant cette intégration :

* Lorsque des ressources d’Adobe Stock sont enregistrées dans AEM, elles deviennent des ressources AEM Assets standard, avec un binaire enregistré dans le référentiel AEM. Certaines métadonnées liées à Adobe Stock sont enregistrées pour la ressource dans AEM. Sinon, le processus d’ingestion ressemble à celui de tout autre fichier. Par exemple, si les balises dynamiques sont actives, les balises sont ajoutées à ces fichiers lors de l’enregistrement.
* La ressource enregistrée dans AEM est une copie et non un lien vers Adobe Stock.

**Utilisation des ressources enregistrées depuis Adobe Stock dans AEM dans Creative Cloud**. Cette intégration est indépendante d’Adobe Asset Link, mais cette fonction reconnaît ces ressources enregistrées depuis Stock de cette manière et affiche d’autres métadonnées et une icône Stock sur ces ressources dans l’interface utilisateur de l’extension Adobe Asset Link dans Photoshop, Illustrator et InDesign. Les fichiers peuvent être parcourus, ouverts , etc., car il s’agit de ressources AEM normales lorsqu’ils sont enregistrés dans AEM.
Les utilisateurs créatifs utilisant des applications Creative Cloud avec l’extension Adobe Asset Link ont accès aux ressources déjà sous licence d’Adobe Stock dans AEM et peuvent aussi utiliser le panneau Bibliothèques Creative Cloud pour rechercher, prévisualiser et attribuer une licence aux ressources Adobe Stock.
Les ressources d’Adobe Stock sous licence et enregistrées dans AEM deviennent accessibles aux équipes élargies qui accèdent au déploiement AEM Assets, tandis que les équipes créatives attribuant une licence aux ressources d’Adobe Stock via le panneau Bibliothèques Creative Cloud les rendent uniquement disponibles pour eux par défaut dans leur compte Creative Cloud.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## A propos du stockage de fichiers dans un DAM {#about-storing-assets-in-a-dam}

Pour établir un workflow efficace entre les équipes créatives et marketing/métier, et sélectionner les meilleures fonctionnalités de prise en charge, il est important de comprendre quand et pourquoi les ressources sont stockées dans la gestion des actifs numériques.

### Pourquoi les ressources sont-elles stockées dans la gestion des actifs numériques ? {#why-assets-are-stored-in-dam}

Le stockage des ressources dans la gestion des actifs numériques permet d’en faciliter l’accès et de les retrouver plus aisément. Cela garantit que les ressources peuvent être exploitées par de nombreux utilisateurs au sein de votre organisation ou écosystème, qui comprend les partenaires, les clients, etc.

La plupart des entreprises choisissent de stocker uniquement les ressources pertinentes pour les processus marketing/métier en aval (publication sur des canaux tels que le canal web via AEM Sites ou d’autres canaux traités par Adobe Experience Cloud : Marketing Cloud, Advertising Cloud et mesurés par Analytics Cloud, satisfaction des besoins des utilisateurs et partenaires, etc.). En outre, les entreprises stockent les ressources qui peuvent être soumises à un processus de révision/approbation dans la gestion des actifs numériques. De cette manière, la gestions des actifs numériques stocke principalement les ressources ayant de grandes chances d’être exploitées, en évitant de stocker les ressources inactives.

Le stockage des ressources est soumis à des considérations techniques et d’utilisation des ressources. La gestion des actifs numériques fournit des services supplémentaires pour les ressources stockées, notamment l’extraction de métadonnées, le contrôle de versions, la génération d’aperçus/de transcodage, la gestion des références et l’ajout d’informations de contrôle d’accès. Ces services utilisent davantage de temps et de ressources de votre infrastructure.

Souvent, le stockage de toutes les ressources et mises à jour n’est pas souhaitable. Par exemple, si les mises à jour de ressources spécifiques sont de mauvaise qualité et utilisent les ressources en excès, les ressources peuvent être stockées dans la gestion des actifs numériques.

#### Quand les ressources sont-elles stockées dans la gestion des actifs numériques ? {#when-assets-are-stored-in-dam}

Les équipes créatives (et les organisations) ne sont généralement pas intéressées par le stockage des ressources à chaque étape de leur cycle de vie. Par exemple, elles évitent de stocker des ressources dans les cas suivants :

* Si les ressources doivent être finalisées ou sont soumises à expérimentation
* Si les ressources ne passent pas le cycle de révision de l’équipe interne/créative
* L’équipe dispose de ressources plus pertinentes que celle en question pour présenter son travail à des équipes externes

En règle générale, les classes de ressources suivantes sont stockées dans la gestion des actifs numériques :

* Les ressources ayant atteint une certaine maturité et que l’on estime prêtes à être partagées
* Les ressources qui ont été présélectionnées par l’équipe créative
* Les formats de ressources spécifiques qui sont utilisables ou demandés par le marketing, selon un contrat ou un accord spécifique (par exemple, des fichiers JPG convertis à partir de fichiers RAW, des TIFF/images à partir d’originaux PSD)

#### Quand les mises à jour de ressources sont-elles stockées dans la gestion des actifs numériques ? {#when-updates-to-assets-are-stored-in-dam}

En règle générale, seules les mises à jour des ressources pertinentes pour un large ensemble d’utilisateurs de la gestion des actifs numériques doivent être stockées dans la gestion des actifs numériques. Cela garantit que les utilisateurs (marketing et fonctions similaires) voient uniquement les versions appropriées dans la chronologie des ressources de la gestion des actifs numériques.

Généralement, il s’agit des modifications en rapport avec les principaux jalons dans le cycle de vie des ressources. Par exemple, la ressource initiale prête pour les marketeurs ou une mise à jour officielle basée sur une demande/révision fournie par l’équipe créative doit être enregistrée et versionnée dans la gestion des actifs numériques.

Il peut s’agir, par exemple, d’une mise à jour de l’équipe créative pour révision par l’équipe marketing après une demande de modification de la ressource existante dans la gestion des actifs numériques. Elle doit être stockée et versionnée dans la gestion des actifs numériques à des fins de référence ou pour revenir à la version précédente.

Voici quelques exemples de mises à jour qui ne sont généralement pas pertinentes :

* Les premières versions des ressources transférées avant qu’elles ne soient prêtes pour révision par le marketing
* Les modifications fréquentes de la ressource par l’équipe créative pendant la phase de travail en cours et avant que l’équipe créative ne décide que la ressource est prête

### Accès des utilisateurs à la gestion des actifs numériques {#user-access-to-dam}

AEM Assets prend en charge deux types d’utilisateurs selon leur accès au déploiement d’AEM Assets. En règle générale, les utilisateurs à l’intérieur du réseau d’entreprise (pare-feu) ont un accès direct à la gestion des actifs numériques. D’autres utilisateurs à l’extérieur du réseau d’entreprise n’auront pas un accès direct. Le type d’utilisateur détermine les intégrations qui peuvent être utilisées du point de vue technique.

#### Utilisateurs créatifs avec un accès direct à la gestion des actifs numériques {#creative-users-with-direct-access-to-dam}

En règle générale, les équipes de création internes, les agences et les professionnels de la création intégrés au réseau interne ont accès à l’instance DAM, y compris la connexion à AEM. AEM et l’infrastructure réseau peuvent être configurés afin d’autoriser un accès direct aux parties externes (généralement, des entreprises de confiance telles que des agences travaillant pour un client) pour disposer d’un accès à AEM via le réseau (par le biais de la liste blanche des adresses IP ou d’un VPN, par exemple).

Dans ce cas, Adobe Asset Link ou l’application de bureau AEM permet d’accéder facilement aux ressources finales/approuvées et vous permet d’enregistrer les ressources prêtes pour les créatifs dans la gestion des actifs numériques.

#### Utilisateurs créatifs sans accès à la gestion des actifs numériques {#creative-users-without-access-to-dam}

Les agences externes et les indépendants sans accès direct à l’instance de la gestion des actifs numériques peuvent avoir besoin de l’accès aux ressources approuvées ou souhaiter ajouter leurs nouvelles créations dans la gestion des actifs numériques.

Utilisez les stratégies suivantes pour fournir un accès aux ressources finales/approuvées :

* Utilisez l’application de bureau si Asset Link ne fonctionne pas.
* Use [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) for distributing assets securely to external partners
* Utilisez une implémentation personnalisée d’un portail de distribution et de source basé sur [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilisez la configuration du contrôle d’accès dans AEM et l’infrastructure réseau nécessaire (mise en liste blanche d’adresses IP et VPN, par exemple) pour permettre aux parties externes d’accéder à une zone de contenu dédiée dans DAM. Ils peuvent utiliser l’interface utilisateur web d’AEM pour obtenir des ressources et télécharger du nouveau contenu dans DAM.

#### Tâche en cours sur les ressources d’AEM {#work-in-progress-on-assets-from-aem}

Comme nous l’avons vu dans ce document, il est recommandé d’effectuer des mises à jour importantes sur les ressources, parfois appelées tâche en cours, sans que toutes les modifications enregistrées dans le fichier local ne soient téléchargées dans AEM en tant que modifications. Cela accélère le travail d’un utilisateur sur poste de travail, limite la bande passante réseau utilisée et maintient le calendrier des ressources ciblé sur les mises à jour majeures et contrôlées.

Adobe Asset Link est adapté à cas d’utilisation :

* Lorsque les utilisateurs de Photoshop, InDesign ou Illustrator souhaitent modifier un fichier, ils effectuent une opération d’extraction sur la ressource donnée.
* La ressource est téléchargée en arrière-plan, placée dans le compte Creative Cloud des utilisateurs synchronisés sur le disque par l’application de bureau Creative Cloud et l’indicateur d’extraction est activé sur la ressource dans AEM afin de minimiser les conflits de modification.
* À ce stade, l’utilisateur utilise un fichier stocké localement dans l’emplacement synchronisé et peut continuer à travailler et à enregistrer les modifications nécessaires selon la fréquence nécessaire.
* De plus, comme la ressource figure dans le compte Creative Cloud, elle est également disponible sur d’autres appareils appartenant à l’utilisateur (par exemple, elle peut être ouverte ou modifiée dans une application mobile Creative Cloud dédiée) et peut être partagée avec d’autres utilisateurs Creative Cloud à des fins de collaboration.
* Lorsque l’utilisateur créatif a terminé d’apporter des modifications, il peut effectuer une opération d’archivage sur ce fichier dans son application Creative Cloud, en fournissant un commentaire facultatif. La ressource correspondante dans AEM est versionnée et mise à jour avec le nouveau binaire. Les utilisateurs d’AEM comme les marketeurs ou les utilisateurs du cœur de métier, ont accès aux modifications importantes des ressources, ou jalons, via l’interface utilisateur de chronologie d’AEM Assets.

L’application de bureau AEM propose un partage réseau pour les ressources ouvertes dans l’application native. Par défaut, toutes les modifications apportées localement sont téléchargées automatiquement dans AEM après un bref instant. Avec une telle configuration, les enregistrements fréquents durant la phase de tâche en cours seraient tous téléchargés dans AEM et versionnés, ce qui créerait un trafic réseau important et des défis d’évolutivité potentiels, sans mentionner les versions inutiles dans AEM.

L’approche recommandée dans ce cas consiste à utiliser une option dans l’application de bureau AEM pour désactiver les mises à jour automatisées et à télécharger manuellement les modifications des ressources dans AEM, en utilisant l’action de téléchargement des modifications dans l’interface utilisateur État de la ressource de l’application.

#### Téléchargement en masse dans la gestion des actifs numériques {#bulk-upload-to-dam}

Dans certains cas, il est possible que vous deviez télécharger simultanément un plus grand nombre de fichiers dans la gestion des actifs numériques, par exemple :

* Transfert des résultats de  photoshoots ou projets plus volumineux
* Transfert de ressources fournies par les agences de création
* Transfert de ressources sélectionnées à partir d’un plus grand ensemble si la sélection est effectuée en dehors de la gestion des actifs numériques

La description fait référence au téléchargement de fichiers de manière opérationnelle (par exemple, toutes les semaines ou avec chaque séance photo), dans le cadre normal du processus de l’utilisateur de bureau. Les migrations de ressources de grande taille ne sont pas abordées ici.

Vous pouvez utiliser les fonctionnalités de transfert suivantes :

* Pour télécharger des dossiers volumineux/hiérarchiques en bloc, utilisez l’application de bureau AEM qui propose une fonctionnalité de [téléchargement de dossiers](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload). Vous pouvez également transférer des structures de dossiers hiérarchiques. Les ressources sont transférées en arrière-plan et, par conséquent, le transfert n’est pas associé à une session du navigateur web.
* Pour télécharger quelques fichiers à partir d’un seul dossier, faites les glisser directement jusqu’à l’interface web ou utilisez l’option Créer dans l’interface web d’AEM Assets.
* Selon les besoins de votre entreprise, vous pouvez également utiliser le chargeur personnalisé.

#### Manage digital assets directly from desktop {#managing-digital-assets-directly-from-desktop}

Si vous utilisez des partages de fichiers réseau pour gérer les ressources numériques, le fait d’utiliser uniquement un partage réseau mappé par l’application de bureau AEM peut être considéré comme une alternative pratique. Si vous choisissez de ne plus utiliser les partages de fichiers réseau, l’interface utilisateur web d’AEM propose un large éventail de fonctionnalités de gestion des actifs numériques qui vont bien au-delà de ce qui est possible sur un partage réseau (recherche, collections, métadonnées, collaboration, aperçus, etc.) et l’application de bureau AEM fournit un lien pratique pour connecter le référentiel de gestion des actifs numériques côté serveur au travail sur l’ordinateur de bureau.

Evitez d’utiliser l’application de bureau AEM pour gérer les ressources directement dans le partage réseau des ressources AEM. Par exemple, évitez d’utiliser l’application de bureau AEM pour déplacer/copier plusieurs fichiers. Au lieu de cela, utilisez l’interface utilisateur web d’AEM Assets pour faire glisser des fichiers à partir du Finder/de l’Explorateur vers le partage réseau ou utilisez la fonctionnalité de transfert de dossier d’AEM Assets.

#### Migration de ressources {#asset-migration}

Pour planifier et exécuter des migrations de ressources depuis le système existant vers un nouveau système ou effectuer une migration d’un gros volumes de ressources stockées sur les serveurs, consultez le [Guide de migration](/help/assets/assets-migration-guide.md). L’application de bureau AEM et les intégrations d’AEM avec Creative Cloud ne prennent pas en charge de telles migrations. En raison des grands volumes de ressources à assimiler et des exigences supplémentaires en termes de mappage, de transformation et d’intégration des métadonnées, les migrations doivent être gérées à l’aide d’outils et d’approches différents.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [Meilleures pratiques pour l’application de bureau AEM](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [AEM Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Intégration d’AEM et d’Adobe Stock](aem-assets-adobe-stock.md)

