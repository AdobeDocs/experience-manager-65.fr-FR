---
title: Concevoir des formulaires HTML5 accessibles
seo-title: Designing accessible HTML5 forms
description: Les formulaires HTML5 utilisent la norme d’accessibilité ARIA HTML5. Ces formulaires prennent en charge la navigation par onglets et sont certifiés compatibles avec les lecteurs d’écran courants.
seo-description: HTML5 forms use the ARIA HTML5 accessibility standard. These forms support tabbed navigation and are certified to be compatible with common screen readers.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 33%

---

# Concevoir des formulaires HTML5 accessibles {#designing-accessible-html-forms}

Les formulaires HTML5 utilisent la norme d’accessibilité ARIA HTML5 pour générer des formulaires HTML accessibles. Ces formulaires prennent en charge la navigation par onglets (sauf Mozilla Firefox) et sont certifiés compatibles avec les lecteurs d’écran les plus courants. Pour générer un formulaire HTML5 avec les fonctions d’accessibilité appropriées, concevez le modèle de formulaire XFA à partir de quelques directives de conception de base. Les directives de conception comprennent la configuration des onglets dans l’ordre approprié et fournissent le contenu du texte vocal pour chaque commande du formulaire. AEM Forms Designer prend en charge le paramètre de ces attributs de commande du formulaire pour générer un formulaire en version PDF et HTML5 accessible.

*Remarque : la navigation par onglets ne couvre pas les champs protégés tels que les champs de calcul affichant la somme des valeurs. Pour que le lecteur d’écran lise la valeur d’un champ protégé, placez un champ Lecture seule vide au-dessus ou en regard du champ protégé. Attribuez la valeur du champ protégé au nouveau champ en lecture seule. Le lecteur d’écran ou la navigation par onglets peut sélectionner ce champ en lecture seule et le définir comme la valeur du champ protégé.*

AEM Forms Designer comprend plusieurs options de texte vocal qui peuvent être transmises aux lecteurs d’écran. Pour chaque objet d’un formulaire, l’utilisateur peut spécifier l’un des paramètres suivants pour le texte du lecteur d’écran :

* Texte du lecteur d’écran personnalisé qui peut être défini à l’aide de la palette Accessibilité. Les auteurs peuvent annoter les noms des boutons et des champs, ainsi que leur rôle.
* Info-bulles, qui peuvent être définies dans la palette Accessibilité.
* Légendes des champs du formulaire.
* Noms des objets, tels que spécifiés dans l’option Nom de l’onglet Liaison.

![Accessibilité](assets/accessibility.png)

Lorsque plusieurs options telles que l’info-bulle, le texte de Reader d’écran et la légende sont disponibles sur un contrôle de formulaire, le Reader d’écran n’utilise qu’une seule de ces propriétés. L’ordre par défaut est Texte de Reader d’écran personnalisé, info-bulle, Légende et Nom. Vous pouvez remplacer cet ordre par défaut à l’aide de l’option **Précédence** du lecteur d’écran dans la palette Accessibilité.
