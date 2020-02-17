---
title: Référence des schémas de métadonnées
description: 'Découvrez les conventions standard permettant de décrire les métadonnées des ressources, y compris Dublin Core, IPTC et d’autres schémas de métadonnées. '
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Metadata schemata reference {#metadata-schemata-reference}

La référence ci-après contient des informations sur un schéma de métadonnées spécifique (dans l’ordre alphabétique) ainsi qu’une liste de propriétés et de leur définition.

## Dublin Core {#dublin-core}

La métadonnée Dublin Core fournit un ensemble de conventions normalisé pour décrire les ressources afin de faciliter leur recherche. Dans AEM Assets, Dublin Core décrit les ressources numériques, y compris les vidéos, le son, les images et les documents.

Le DCMES (Dublin Core Metadata Element Set) contient 15 éléments de métadonnées qui sont répertoriés dans le tableau ci-après. Chaque élément Dublin Core est facultatif et peut être utilisé plusieurs fois. Vous pouvez ajouter ou supprimer des informations de métadonnées Dublin Core comme vous le feriez pour les métadonnées spécifiques au type de média.

Outre le DCMES, il existe d’autres éléments de métadonnées créés par le Dublin Core Initiative. Pour plus d’informations, voir [Dublin Core Initiative](https://dublincore.org/).

| Propriétés | Description |
|---|---|
| contributor | Personne ou entreprise chargée d&#39;apporter des contributions au contenu. |
| coverage (couverture) | Emplacement géographique ou période que couvre la ressource. |
| creator (créateur) | Personne ou entreprise chargée de la création du contenu. |
| date | Date ou période associée à la ressource. |
| description | Informations supplémentaires sur la ressource. |
| format | Format de fichier, support physique ou dimensions de la ressource. AEM utilise le format dc:format pour indiquer le type MIME de la ressource. |
| formulaire | Référence unique à la ressource. |
| language | Langue de la ressource (&quot;en&quot; pour l&#39;anglais, par exemple). |
| publisher (éditeur) | Personne ou entreprise chargée de rendre la ressource disponible. |
| relation | Ressource connexe. |
| rights (droits) | Informations sur la personne qui dispose des droits sur cette ressource. |
| source | Ressource connexe à partir de laquelle la ressource est dérivée. |
| subject (objet) | Objet de la ressource. |
| titre | Nom de la ressource. |
| Type | Nature ou genre de la ressource. |

## IPTC {#iptc}

L’ITPC (International Press Telecommunications Council) est un consortium réunissant les principales agences de presse à travers le monde. L’un de ses principaux objectifs est de développer et maintenir des normes techniques. L’IPTC a défini un ensemble de normes de métadonnées photographiques qui est presque universellement accepté par les photographes. Ces normes de métadonnées faisaient partie de la norme plus générale appelée IPTC Information Interchange Model (IIM) créée dans les années 1990.

Bien que les informations d’en-tête IPTC ont été essentiellement remplacées par XMP, un schéma de base IPTC et un schéma d’extension sont disponibles pour XMP. Dans les programmes de traitement d’images, les propriétés XMP et IPTC sont synchronisées.
