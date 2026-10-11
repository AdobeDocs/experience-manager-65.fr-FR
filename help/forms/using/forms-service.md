---
title: Service Forms
description: L’article décrit le service Forms et les tâches liées aux formulaires que vous pouvez effectuer à l’aide de ce service.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,Forms Service,PDF Generator
exl-id: 6580fe6f-3cdb-45ec-8ba3-51dc60d1965e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b59c0486-3350-52ed-8816-e0a8e11486b8
    internal-label: Forms Service
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 100%
---
# Service Forms {#forms-service}

## Présentation {#overview}

Le service Forms permet de créer des applications clientes interactives de capture de données assurant la validation, le traitement, la transformation et la transmission de formulaires généralement créés dans Designer. Il restitue sous forme de documents PDF toute conception de formulaire que vous créez.

Le service Forms permet également aux organisations d’étendre leurs processus de capture de données intelligentes en déployant des formulaires électroniques au format PDF Adobe. Vous pouvez également utiliser le service pour importer et exporter des données de et vers les formulaires PDF existants, respectivement.

Utilisez le service Forms pour effectuer les opérations suivantes :

* Rendu des formulaires PDF d’après le modèle et les données XML.
* Intégration de données de formulaire pour importer des données dans des formulaires PDF et les en extraire.
* Rendu des formulaires basés sur des fragments.

## Création de formulaires PDF  {#creating-pdf-forms-nbsp}

Utilisez le service Forms pour créer des formulaires PDF pour la capture de données. En général, vous commencez avec un modèle AEM Forms Designer. Utilisez l’opération `renderPDFForm` (lien vers Javadoc) du service Forms pour convertir ce modèle en formulaire PDF.

Le premier paramètre de l’opération `renderPDFForm` est le nom du fichier de modèle (par exemple, `ExpenseClaim.xdp`). Vous pouvez stocker le fichier de modèle dans un système de fichiers local, un référentiel CRX ou à un emplacement HTTP ou FTP. Vous pouvez spécifier l’emplacement du fichier de modèle en définissant la racine du contenu dans le paramètre `PDFFormRenderOptions` de l’opération `renderPDFForm`. Voir la documentation Javadoc pour en savoir plus sur les autres options que vous pouvez spécifier pour le paramètre `PDFFormRenderOptions`.

L’opération `renderPDFForm` peut également accepter des données XML. Les données XML sont fusionnées avec le modèle lors de la création d’un formulaire PDF. Le formulaire PDF généré contient ainsi les données spécifiées. Le deuxième paramètre pour l’opération `renderPDFForm` peut accepter un objet de document (Javadoc) qui contient des données XML.

## Extraction de données des formulaires PDF  {#extracting-data-from-pdf-forms-nbsp}

Utilisez l’opération `exportData` (Javadoc) du service Forms pour extraire les données XML d’un formulaire PDF. Cette opération accepte un document comme son premier paramètre. Vous pouvez exporter les données au format de document XDP ou de fichier XML. Si vous exportez des données au format XML, les données exportées suppriment l’enveloppe XDP et renvoient un fichier XML brut. Vous pouvez spécifier cet arrangement à l’aide du second paramètre.

## Importation des données dans les formulaires PDF {#importing-data-into-pdf-forms}

Le service Forms vous permet de fusionner un formulaire PDF créé en utilisant AEM Forms Designer ou l’opération `renderPDFForm` avec des données XML. L’opération `importData` (Javadoc) du service Forms accepte le formulaire PDF et les données XML et renvoie un formulaire PDF avec des données XML.

## Rendu de formulaires reposant sur des fragments {#rendering-forms-based-on-fragments}

Le service Forms peut restituer des formulaires reposant sur des fragments que vous créez à l’aide d’Adobe AEM Forms Designer. Un fragment est une partie réutilisable d’un formulaire. Il est enregistré sous la forme d’un fichier XDP distinct qui peut être inséré dans plusieurs conceptions de formulaire. Un fragment peut très bien inclure un bloc d’adresse ou un paragraphe juridique, par exemple.

L’utilisation de fragments simplifie et accélère la création et la gestion d’un grand nombre de formulaires. Lorsque vous créez un formulaire, insérez une référence au fragment requis pour que ce dernier apparaisse dans le formulaire. La référence au fragment contient un sous-formulaire pointant vers le fichier XDP physique.

L’utilisation de fragments présente les avantages suivants :

* **Réutilisation du contenu** : vous pouvez réutiliser du contenu dans plusieurs conceptions de formulaire. Pour réutiliser rapidement des portions d’un même contenu dans plusieurs formulaires, créez un fragment. La copie ou la recréation du contenu prend plus de temps. L’emploi de fragments permet par ailleurs de garantir l’homogénéité du contenu et de l’aspect de parties de formulaire reprises dans les différents formulaires de référencement.
* **Mises à jour globales** : vous pouvez apporter des changements généraux à plusieurs formulaires simultanément en effectuant cette opération une fois dans un seul fichier. Lorsque vous modifiez le contenu, les objets de script, les liaisons de données, la disposition ou les styles d’un fragment, tous les formulaires XDP faisant référence à ce fragment sont modifiés en conséquence.
* **Création de formulaires partagée** : vous pouvez partager la création de formulaires entre plusieurs ressources. Les développeurs de formulaires familiarisés avec le scripting ou d’autres fonctionnalités avancées d’AEM Forms Designer peuvent développer et partager des fragments qui utilisent le scripting et des propriétés dynamiques. Les concepteurs et conceptrices peuvent créer des formulaires à partir des fragments. En outre, ils ou elles peuvent utiliser les fragments pour s’assurer que toutes les parties d’un formulaire ont une apparence et une fonctionnalité cohérentes dans plusieurs formulaires.
