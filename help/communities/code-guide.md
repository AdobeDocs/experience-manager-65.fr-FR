---
title: Consignes de codage
seo-title: Consignes de codage
description: Conseils, astuces et astuces pour les développeurs de communautés
seo-description: Conseils, astuces et astuces pour les développeurs de communautés
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 4%

---


# Consignes de codage {#coding-guidelines}

## Instructions, conseils et astuces {#guidelines-tips-and-tricks}

L’utilisation de AEM Communities a évolué, passant d’une dépendance importante à l’égard des pages Java Server à une flexibilité dans le choix de langages de script de modèles où la logique métier, le style et le contenu des pages sont distincts les uns des autres.

L’API SocialResourceProvider offre une plus grande flexibilité dans l’utilisation du contenu généré par l’utilisateur, ce qui évite de devoir connaître l’option [SRP](srp.md) choisie pour le déploiement.

Vous trouverez ci-dessous diverses directives de codage et les meilleures pratiques pour les développeurs AEM Communities :

### Code {#code}

* [Accès à l&#39;UGC avec SRP](accessing-ugc-with-srp.md) : comment éviter d&#39;écrire une application qui ne fonctionne que lorsque l&#39;UGC est stocké dans JCR (JSRP).
* [SocialUtils Refactoring](socialutils.md) - méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
* [Conventions](naming-conventions.md) de dénomination - conventions de dénomination pour les classes Java personnalisées.

### Scripts {#scripts}

* [Téléchargement partiel des composants](sideloading.md) de communautés : comment ajouter dynamiquement un composant après le chargement de la page.
* [Rich Text Editor Essentials](rte.md) - Comment personnaliser l’interface utilisateur de texte enrichi fournie aux membres pour la publication de contenu.

### IDE {#ide}

* [Utilisation de Maven pour les communautés](maven.md) : comment inclure le fichier jar de l&#39;API Communautés.
* [SocialUtils Refactoring](socialutils.md) - méthodes d’utilitaire pour SRP qui remplacent SocialUtils.

