---
title: Envoi sécurisé de gros volumes d’information
description: Document Security prend en charge l’association de licences avec des utilisateurs et utilisatrices, plutôt qu’avec des documents dans les environnements de production de masse.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 92%

---

# Envoi sécurisé de gros volumes d’information {#high-volume-secure-information-delivery}

Dans un environnement de production de masse, tel que celui qui génère des factures mensuelles sécurisées pour une société de télécommunications, la création de licences spécifiques à chaque document peut devenir un processus gourmand en ressources. Dans ce cas, Document Security prend en charge l’association de licences avec les utilisateurs et utilisatrices plutôt qu’avec les documents. La licence générée pour un utilisateur ou une utilisatrice est utilisée pour tous les documents protégés de cette personne.

L’un des avantages de cette approche est que la taille de la base de données Document Security ne s’accroît pas de manière linéaire avec les documents, mais avec le nombre d’utilisateurs. En outre, puisque vous ne créez la licence qu’une seule fois par personne, la protection ultérieure des documents par le biais de ces politiques est accélérée. Des fonctionnalités telles que l’accès hors ligne, l’expiration du document et la révocation sont prises en charge pour tous ces documents.

Document Security prend également en charge les politiques abstraites. Les politiques abstraites sont des modèles de politique qui contiennent tous les attributs de politique, tels que les paramètres de Document Security et les droits d’utilisation, mais ne contiennent pas de liste d’entités de sécurité. Les équipes d’administration peuvent créer un nombre illimité de politiques à partir de la politique abstraite avec différentes entités de sécurité qui doivent avoir accès aux documents. Les modifications apportées à la politique abstraite n’affectent pas les politiques réelles générées à partir des politiques abstraites.

Si une société de télécommunications applique une génération de factures mensuelle, vous créez une politique abstraite, puis des utilisateurs et utilisatrices, et vous générez des licences uniques pour chaque personne. Les licences sont ensuite appliquées aux documents pour chaque personne.

La création d’une politique abstraite est prise en charge uniquement par le biais du SDK Java de Document Security. Vous pouvez toutefois administrer les politiques que vous créez à partir de la politique abstraite des pages web de Document Security. Les politiques créées à l’aide de cette méthode ont un comportement identique à celui des politiques créées à partir des pages web de Document Security.

Pour plus d’informations, consultez [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).
