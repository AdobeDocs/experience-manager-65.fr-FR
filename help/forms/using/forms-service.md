---
title: Service Forms
seo-title: Service Forms
description: Cet article décrit le service Forms et les tâches relatives aux formulaires que vous pouvez effectuer à l’aide de ce service.
seo-description: Cet article décrit le service Forms et les tâches relatives aux formulaires que vous pouvez effectuer à l’aide de ce service.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
exl-id: bd1216e4-2248-484b-a3c1-c209da4ff94f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 83%

---

# Service Forms {#forms-service}

## Présentation {#overview}

Le service Forms permet de créer des applications clientes interactives de capture de données assurant la validation, le traitement, la transformation et la transmission de formulaires généralement créés dans Designer. Il restitue sous forme de documents PDF toute conception de formulaire que vous créez.

Le service Forms permet aux entreprises de développer leurs processus de capture intelligente de données en déployant des formulaires électroniques au format PDF d’Adobe. Vous pouvez également utiliser le service pour importer et exporter des données de et vers les formulaires PDF existants, respectivement.

Utilisez le service Forms pour effectuer les opérations suivantes :

* Rendu des formulaires PDF d’après le modèle et les données XML.
* Intégration de données de formulaire pour importer des données dans des formulaires PDF et les en extraire.
* Rendu des formulaires reposant sur des fragments.

## Création de formulaires PDF  {#creating-pdf-forms-nbsp}

Utilisez le service Forms pour créer des formulaires PDF pour la capture de données. En général, vous commencez avec un modèle AEM Forms Designer. Utilisez l’opération `renderPDFForm` (lien vers Javadoc) du service Forms pour convertir ce modèle en formulaire PDF.

Le premier paramètre de l’opération `renderPDFForm` est le nom du fichier de modèle (par exemple, `ExpenseClaim.xdp`. Vous pouvez stocker le fichier de modèle dans un système de fichiers local, un référentiel CRX ou à un emplacement HTTP ou FTP. Vous pouvez spécifier l’emplacement du fichier de modèle en définissant la racine du contenu dans le paramètre `PDFFormRenderOptions` de l’opération `renderPDFForm`. Voir la documentation Javadoc pour en savoir plus sur les autres options que vous pouvez spécifier pour le paramètre `PDFFormRenderOptions`.

L’opération `renderPDFForm` peut également accepter des données XML. Les données XML sont fusionnées avec le modèle lors de la création d’un formulaire PDF afin que le formulaire PDF généré contienne les données spécifiées. Le deuxième paramètre pour l’opération `renderPDFForm` peut accepter un objet de document (Javadoc) qui contient des données XML.

## Extraction de données des formulaires PDF  {#extracting-data-from-pdf-forms-nbsp}

Utilisez l’opération `exportData` (Javadoc) du service Forms pour extraire les données XML d’un formulaire PDF. Cette opération accepte un document comme son premier paramètre. Vous pouvez exporter les données au format de document XDP ou de fichier XML. Si vous exportez des données au format XML, les données exportées suppriment l’enveloppe XDP et renvoient un fichier XML brut. Vous pouvez spécifier cet arrangement à l’aide du second paramètre.

## Importation des données dans les formulaires PDF  {#importing-data-into-pdf-forms}

Le service Forms vous permet de fusionner un formulaire PDF créé en utilisant AEM Forms Designer ou l’opération `renderPDFForm` avec des données XML. L’opération `importData` (Javadoc) du service Forms accepte le formulaire PDF et les données XML et renvoie un formulaire PDF avec des données XML.

## Rendu de formulaires reposant sur des fragments {#rendering-forms-based-on-fragments}

Le service Forms peut restituer des formulaires reposant sur des fragments que vous créez à l’aide d’Adobe AEM Forms Designer. Un fragment est une partie réutilisable d’un formulaire. Il est enregistré dans un fichier XDP distinct qui peut être inséré dans plusieurs conceptions de formulaire. Un fragment peut très bien inclure un bloc d’adresse ou un paragraphe juridique, par exemple.

L’utilisation de fragments simplifie et accélère la création et la gestion d’un grand nombre de formulaires. Lors de la création d’un formulaire, insérez une référence au fragment requis pour que le fragment s’affiche dans le formulaire. La référence au fragment contient un sous-formulaire pointant vers le fichier XDP physique.

L’utilisation de fragments présente les avantages suivants :

* **Réutilisation du contenu** : vous pouvez réutiliser du contenu dans plusieurs conceptions de formulaire. Pour réutiliser rapidement des portions d’un même contenu dans plusieurs formulaires, créez un fragment. La copie ou la recréation du contenu prend plus de temps. L’emploi de fragments permet par ailleurs de garantir l’homogénéité du contenu et de l’aspect de parties de formulaire reprises dans les différents formulaires de référencement.
* **Mises à jour globales** : vous pouvez apporter des changements généraux à plusieurs formulaires simultanément en effectuant cette opération une fois dans un seul fichier. Vous pouvez modifier le contenu, les objets de script, les liaisons de données, la disposition ou les styles d’un fragment. Tous les formulaires XDP référençant ce fragment reflètent ces changements.
* **Création de formulaires partagée** : vous pouvez partager la création de formulaires entre plusieurs ressources. Les développeurs de formulaires maîtrisant les fonctions de script ou d’autres fonctions avancées d’AEM Forms Designer peuvent développer et partager des fragments utilisant des fonctions de script et des propriétés dynamiques. Les concepteurs peuvent créer des formulaires à partir des fragments. En outre, ils peuvent utiliser les fragments pour s’assurer que l’aspect et la fonctionnalité de tous les éléments d’un formulaire sont cohérents dans plusieurs formulaires.
