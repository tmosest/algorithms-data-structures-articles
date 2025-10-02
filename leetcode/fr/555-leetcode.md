---
titre: LeetCode 555. Chaînes concaténées de Split -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
**Réponse**

Le problème de concaténation de la rotation est en fait un problème classique de manipulation des chaînes – le problème de rotation **minimum (lexicographiquement le plus petit)** (parfois appelé déplacement cyclique le plus petit* ou déplacement cyclique minimal*).

La façon standard de le résoudre est de joindre d'abord toutes les pièces en une seule longue chaîne (par exemple, "BABC" pour la liste `['B','AB','C']`). Ensuite, vous exécutez un algorithme linéaire de temps comme l'algorithme ** de Booths** (ou utilisez une approche suffixe-array/rolling-hash) pour trouver l'index de la plus petite rotation lexicographique de cette chaîne concaténée. La rotation à partir de cet indice est l'unique ordre valide que vous recherchez.

Si, pour une raison quelconque, vous voulez seulement considérer les rotations qui commencent sur une limite de mot (de sorte que les mots ne sont pas fractionnés), vous testez simplement chacune des rotations possibles de N (chaque mot devient la première pièce) et choisissez la plus petite lexicographie. Ceci est trivial à faire en temps O(N·L) (ou avec un algorithme de style Booth limité aux positions de démarrage N).

En bref, le problème est le problème de la rotation lexicographique **minimale** (ou du déplacement cyclique le plus lent) et il peut être résolu dans le temps linéaire par l'algorithme de Booths (ou équivalent par un doublement de chaîne avec un suffixe-array, un suffixe-tree, ou même une comparaison de force brute pour un petit N).