---
title: La génération de PDF ne parvient pas à imprimer un grand nombre de PDF avec WorkBench.
description: Lorsqu’une personne génère un grand nombre de PDF via des services implémentés par le biais de WorkBench, le service d’impression échoue.
exl-id: f3746b8e-4c38-447a-b5bf-d11fc77556f7
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '775'
ht-degree: 100%

---

# La génération de PDF ne parvient pas à imprimer un grand nombre de PDF via WorkBench. {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## Problème {#issue}

Lorsqu’une personne génère un grand nombre de PDF via des services implémentés par le biais de WorkBench. Le service échoue en raison d’une mémoire insuffisante. L’erreur se produit comme suit :

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

En effet, le nombre maximal de pages dans une requête d’impression est limité à environ 1 000 pages sous Windows. Lorsqu’une sortie d’impression est générée, le modèle et les données doivent être chargés en mémoire et la disposition qui en résulte est assemblée en mémoire. Cela signifie qu’il existe des limites à la taille de la sortie finale. Le processus qui génère la sortie d’impression est une tâche 32 bits, ce qui signifie qu’elle est limitée à 2 Go de RAM sous Windows <!--and 4 GB on UNIX-->.

## Application {#applies-to}

La solution s’applique à AEM Forms <!--JEE Server and AEM Forms on OSGi Server--> pour x86_win32 XMLFM.

## Solution {#solution}

Le facteur le plus important affectant l’utilisation de la mémoire est la quantité de données sur un formulaire. Cependant, il existe d’autres facteurs dans une conception de formulaire qui affectent l’utilisation de la mémoire à un degré moindre. Lorsque vous avez conscience de ces facteurs, vous pouvez concevoir un formulaire pour une sortie d’impression plus volumineuse. La section suivante indique, par ordre de priorité, les facteurs qui influencent l’empreinte mémoire :

### Facteur d’impact {#impact-factor}

**Élevé**

1. **Sous-formulaires de choix** - Un jeu de sous-formulaires de choix est une variante de l’objet de jeu de sous-formulaires qui vous permet de personnaliser l’affichage de certains sous-formulaires du jeu à l’aide d’instructions conditionnelles.
1. **Utiliser du texte statique à la place des légendes** - Presque tous les champs fournissent une légende interne, la personne doit l’utiliser au lieu d’avoir un texte statique supplémentaire comme légende.
1. Utilisez le **Format de texte enrichi (RTF)** dans la mesure du possible.

**Moyen**

Autres facteurs à prendre en compte lors de la conception d’un modèle de formulaire pour améliorer l’utilisation de la mémoire :

1. Évitez d’utiliser du texte statique pour étiqueter un champ. Utilisez plutôt des légendes dans le champ de texte.
2. N’utilisez pas de Rectangles, Lignes, Objets et Tableaux de manière excessive.
3. Si possible, évitez d’utiliser des sous-formulaires RichText et de choix.
4. Évitez l’utilisation excessive de sous-formulaires et de sous-formulaires imbriqués.

### Limite de taille des données {#data-size-limitations}

Comme il existe une limite de mémoire de processus maximale et que la mémoire consommée par le processus ne dépend pas seulement de la taille du fichier de données. Cela est très étroitement lié à la conception de formulaire et, dans une certaine mesure, à la quantité réelle de données fusionnées dans le formulaire.

Si le formulaire contient de nombreux petits nœuds avec des données de petite taille, le processus consomme plus de mémoire (et donc provoque une insuffisance de mémoire plus rapidement), qu’un formulaire comportant moins de nœuds (même) avec des données volumineuses.

Lisez l’[annexe ci-dessous](#appendix) pour plus d’informations, où les résultats du test sont basés sur le formulaire d’impression (PDF non balisé). L’utilisation de la mémoire de processus de PDF balisé augmente. Cela dépend également du nombre de champs dans le formulaire. Pour faire simple, l’exigence de mémoire de processus serait un peu plus de 1,5 fois supérieure à celle du PDF non balisé.

### Formulaires interactifs {#interactive-forms}

Les formulaires interactifs consomment plus de mémoire que les formulaires d’impression, car les champs interactifs sont rendus à nouveau. Dans les tests réalisés, la consommation de mémoire a été multipliée par 1,5 environ par rapport aux formulaires d’impression, et il s’agissait de formulaires interactifs statiques.

### Formats d’image {#image-formats}

Adobe ne recommande aucun format d’image spécifique. Mais il serait préférable d’avoir une plus petite taille d’image, par exemple, PNG (Portable Network Graphics). Il n’est pas non plus conseillé d’utiliser des images à haute résolution dont la taille varie jusqu’à plusieurs centaines de mégaoctets. En outre, il n’est pas conseillé d’utiliser des images compressées dont la taille lors de la décompression atteint plusieurs centaines de mégaoctets de données.

### Annexe {#appendix}

**Exemples de tableau**

Les différentes variantes d’un tableau ci-dessous présentent le nombre de pages de rendu par rapport à la taille des données pour un tableau simple et un tableau complexe.

1. Un tableau avec une seule colonne où 5 000 pages de PDF sont générées, un fichier de données de 24 Mo et des enregistrements de 30 Ko.

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. Un tableau comportant de nombreuses petites colonnes où 800 pages de PDF sont générées, un fichier de données de 4,6 Mo et des enregistrements de 20 Ko.
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. Un tableau comportant de nombreuses petites colonnes, mais un fichier de données plus volumineux en raison de l’utilisation de noms xmlTag plus volumineux.
Ici, tout est identique au tableau précédent, mais les noms des balises xml sont devenus volumineux (de sorte que la taille du fichier de données augmente sans aucune augmentation des données actives réelles), le résultat final (limite supérieure) est presque identique. Bien que la taille du fichier de données soit passée de 4,6 Mo à 44,6 Mo. Ici, 800 pages de PDF sont générées, la taille du fichier de données est de 44,6 Mo et celle des enregistrements est de 20 Ko.

   ![table_bigger_xml_tagname](/help/forms/using/assets/table_bigger_xml_tagname.png)

Il est donc difficile d’appliquer une limite supérieure générale à la taille du fichier de données. Chaque formulaire est unique. Par conséquent, la consommation de mémoire diffère d’un formulaire à l’autre.
