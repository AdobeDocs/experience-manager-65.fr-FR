---
title: Éditeur d’image
description: L’éditeur d’image est un élément d’AEM essentiel qui peut être utilisé par les composants pour faciliter la manipulation des images par les auteurs de contenu.
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 84%

---

# Éditeur d’image{#image-editor}

L’éditeur d’image est un élément d’AEM essentiel qui peut être utilisé par les composants pour faciliter la manipulation des images par les auteurs de contenu.

>[!CAUTION]
>
>Pour pouvoir utiliser les fonctionnalités de l’éditeur d’image décrites dans cet article, vous devez installer le [pack de fonctionnalités 24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267).

## Unités relatives pour la zone cliquable {#relative-units-for-image-map}

L’éditeur d’image conserve les zones cliquables comme unités absolues et relatives. Les unités relatives sont utiles lorsqu’elles sont fournies en tant qu’attributs de données pour redimensionner de manière dynamique une zone cliquable (par rapport à la taille de l’image) côté client dans un composant d’image réactif.

### Propriété imageMap {#imagemap-property}

Les coordonnées de la zone cliquable sont conservées dans le JCR comme propriété `imageMap` par l’éditeur d’image. Leur format est le suivant.

La propriété stocke des zones comme suit :

`[area1][area2][...]`

Format de zone :

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Exemple :

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Prise en charge des images SVG {#support-for-svg-images}

Les images SVG (Scalable Vector Graphics) sont pris en charge par l’éditeur d’image.

* Les opérations de glisser-déplacer d’une ressource SVG à partir de DAM et le chargement d’un fichier SVG depuis un système de fichiers local sont pris en charge.

## Activation de modules par type MIME {#enabling-plugins-by-mime-type}

Dans certaines situations, les actions de création doivent être restreintes pour certains types MIME en raison de l’absence de prise en charge du traitement côté serveur. Par exemple, la modification d’images SVG n’est peut-être pas autorisée.

Les modules de l’éditeur d’image peuvent être activés de manière sélective par type MIME en définissant une propriété `supportedMimeTypes` sur le nœud de configuration du module donné.

### Exemple {#example}

Par exemple, supposons que la possibilité de recadrer ne doive être accordée que pour les images GIF, JPEG, PNG, WEBP et TIFF.

La propriété `supportedMimeTypes` doit alors être définie sous la forme d’une chaîne des types MIME autorisés sur le nœud de configuration du module sur le nœud `cq:editConfig` du composant d’image.

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
