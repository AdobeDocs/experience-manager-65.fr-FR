---
title: Consignes de codage
seo-title: Consignes de codage
description: Conseils, astuces et conseils pour les développeurs de communautés
seo-description: Conseils, astuces et conseils pour les développeurs de communautés
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 4%

---

# Consignes de codage {#coding-guidelines}

## Conseils, conseils et astuces {#guidelines-tips-and-tricks}

L’utilisation d’AEM Communities est passée d’une dépendance importante à Java Server Pages à une flexibilité dans le choix de langages de script de modèle dans lesquels la logique commerciale, le style et le contenu de page sont différents les uns des autres.

L’API SocialResourceProvider offre une plus grande flexibilité pour l’utilisation du contenu généré par l’utilisateur, ce qui évite de devoir savoir quelle option [SRP](srp.md) a été sélectionnée pour le déploiement.

Vous trouverez ci-dessous diverses instructions de codage et bonnes pratiques pour les développeurs AEM Communities :

### Code {#code}

* [Accès au contenu créé par l’utilisateur avec SRP](accessing-ugc-with-srp.md)  : comment éviter d’écrire une application qui ne fonctionne que lorsque le contenu créé par l’utilisateur est stocké dans JCR (JSRP).
* [SocialUtils Refactoring](socialutils.md)  : méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
* [Conventions de dénomination](naming-conventions.md)  : conventions de dénomination pour les classes Java personnalisées.

### Scripts {#scripts}

* [Chargement dynamique des composants](sideloading.md)  de communauté : comment ajouter dynamiquement un composant après le chargement de la page.
* [Principes de base de l’éditeur de texte enrichi](rte.md)  : comment personnaliser l’interface utilisateur de texte enrichi fournie aux membres pour la publication de contenu.

### IDE {#ide}

* [Utilisation de Maven pour Communities](maven.md)  - Comment inclure le fichier jar de l’API Communities.
* [SocialUtils Refactoring](socialutils.md)  : méthodes d’utilitaire pour SRP qui remplacent SocialUtils.
