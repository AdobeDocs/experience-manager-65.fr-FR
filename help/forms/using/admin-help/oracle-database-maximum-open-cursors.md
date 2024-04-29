---
title: Nombre maximal de curseurs ouverts dans une base de données Oracle
description: Découvrez comment configurer une valeur maximale pour les curseurs ouverts dans Oracle.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '82'
ht-degree: 100%

---

# Nombre maximal de curseurs ouverts dans une base de données Oracle {#oracle-database-maximum-open-cursors-threshold}

Pour configurer une valeur maximale pour les curseurs ouverts dans Oracle, vous devrez peut-être ajuster cette valeur à un nombre approprié pour votre application. Il apparaît qu’avec une charge de taille moyenne, le nombre moyen de curseurs ouverts était de 2700. Il est recommandé de commencer par une limite supérieure fixée à 3000. Pour plus d’informations, rendez-vous sur [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758).
