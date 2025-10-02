---
titre: LeetCode 2469. Convertir la température -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2469. Convertir la température – un guide de solution complet
*(LeetCode #2469, Facile – 0 ms en Java, Python et C++)*

---

TL;DR
- **Problème**: Conversion d'une valeur Celsius en Kelvin et Fahrenheit.
- **Formulaire**
- *Kelvin* = *Celsius* + 273.15
- *Fahrenheit* = *Celsius* × 1,80 + 32,00
- **Complexité**: **O(1)** temps, **O(1)** espace.
- **Langues**: Java, Python, C++ (tous les 0 ms sur LeetCode).

> **Pourquoi est-ce un bon sujet de discussion? * *
> Le problème est un exemple parfait de la façon dont une solution claire et concise peut être exprimée dans n'importe quelle langue. Il montre que vous comprenez les mathématiques de base, la précision des points flottants et l'importance du code propre – toutes les compétences clés pour un rôle d'ingénierie logiciel.

---

Aperçu du problème

> **Input**
> `double celsius` – numéro flottant non négatif (0 ≤ celsius ≤ 1000), arrondi à deux décimales.

> ** Sortie**
> Un tableau `ans = [kelvin, fahrenheit]` où:
> * `kelvin` = `celsius + 273.15`
> * `fahrenheit` = `celsius * 1.80 + 32.00`

> ** Précision** : Les réponses dans les 10 à 5 de la valeur réelle sont acceptées.

---

## --Détails clés

Aspect du bien
- C'est quoi ?
**Complexité du problème**=Les maths rectilignes, pas de structures de données== Nécessite une manipulation soigneuse de l'arrondi des points flottants==La suringénierie avec les classes d'aide est inutile==
**Mise en œuvre**= Formules monolignes, code minimal= Éviter les constantes de précision codées en dur qui peuvent casser sur de nouveaux cas de test== L'utilisation d'une boucle ou d'une récursion pour une seule conversion est exagérée==
Tester les valeurs limites (0, 1000) Tester les nombres négatifs si les contraintes changent

---

Code complet (Java, Python, C++)

> **Toutes les solutions fonctionnent dans l'espace O(1) et O(1). **

---

### Java (Code Leet)

"Java
- 2469. Convertir la température
// Java 17 – 0 ms, 39,9 Mo

solution de classe publique {
public double[] conversionTempérature(double celsius) {
// Formules de conversion de température
double kelvin = celsius + 273,15;
double fahrenheit = celsius * 1,80 + 32,0;

retour de nouveau double[]{kelvin, fahrenheit};
}
}
«» "

> **Pourquoi c'est optimal* *
> - Affectation directe, pas de boucle.
> - Utilise Javas primitive `double` pour la représentation exacte des points flottants.
> - Aucun objet supplémentaire → efficace en mémoire.

---

Python 3

'`python
# 2469. Convertir la température
# Python 3 – 0 ms, 15.3 Mo

Solution de classe:
def convertTempérature(self, celsius: float) -> list[float]:
kelvin = celsius + 273,15
fahrenheit = celsius * 1,80 + 32,0
retour [kelvin, fahrenheit]
«» "

> **Tricks de python* *
> - Les conseils de type (`float` → `list[float]`) aident les IDE et les analyseurs statiques.
> - Liste littérale `[kelvin, fahrenheit]` est concise et claire.

---

C++17

'`cpp
- 2469. Convertir la température
// C++17 – 0 ms, 10,9 Mo

solution de classe {
public:
vecteur<double> convertirTempérature(double celsius) {
double kelvin = celsius + 273,15;
double fahrenheit = celsius * 1,80 + 32,0;
retour {kelvin, fahrenheit};
}
};
«» "

> **C++ faits saillants* *
> - `vector<double>` est le type de retour requis par LeetCode.
> - Pas d'allocation dynamique – la liste des initialisateurs crée le vecteur en place.

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
Calcul du "kelvin"
Calcul du "fahrenheit"
Autres Création du tableau de résultats/vecteur

L'algorithme est à temps constant et à espace constant car il effectue un nombre fixe d'opérations arithmétiques, quelle que soit la valeur d'entrée.

---

## ☐ Cas de bord et stratégie d'essai

Autres Cas d'essai
C'est quoi ?
«celsius = 0» ; doit retourner «[273.15, 32]». Autres
"celsius = 1000" , sans débordement. Autres
"celsius = 36,5" Valeur typique; correspond à l'exemple de LeetCode. Autres
Un autre exemple de la déclaration. Autres
**Point flottant**: «celsius = 0,01» vérifie la précision près de zéro. Autres

**Conseil:** Utilisez `assert` ou un cadre de test unitaire (JUnit, PyTest, GoogleTest) pour automatiser ces vérifications.

---

## Description en-depth

C'est pas vrai. Les mathématiques

- **Kelvin**: échelle de température compensée par 273.15, donc "K = C + 273.15".
- **Fahrenheit**: Échelle avec un multiplicateur et un décalage différents: `F = C × 1,8 + 32`.

Les deux formules sont dérivées de transformations linéaires et ne nécessitent que de l'arithmétique de base.

Considérations de précision

- LeetCode accepte une erreur absolue ≤ 10−5, de sorte que la précision "double" (15 décimales) est plus que suffisante.
- Éviter d'utiliser "float" parce qu'il peut introduire des erreurs d'arrondi pour des valeurs comme "122.11".

C'est vrai. Style de codage

- **Explicité**: La désignation de variables (`kelvin`, `fahrenheit`) améliore la lisibilité.
- **Compact**: La logique s'inscrit dans une seule ligne par conversion, démontrant un codage concis.
- **No Magic Numbers**: Les constantes `273.15` et `1.80` sont les valeurs de conversion standard; commentez-les si l'intervieweur préfère des explications explicites.

---

Article du blog – Convertissez la température : une feuille d'entretien

> **Cible auprès du public**: Ingénieurs logiciels se préparant pour les interviews de codage, recruteurs à la recherche de code propre, étudiants désireux de pratiquer LeetCode.

---

Titre
**Convertir la température – LeetCode 2469 expliqué (Java, Python, C++) – Un démarrage rapide pour la réussite de l'entrevue**

Description de la méta
Découvrez comment résoudre le LeetCode 2469 Convertissez la température en Java, Python et C++ avec des solutions O(1) propres. Augmentez votre confiance en l'interview et atterrissez votre travail de rêve!

Rubriques (friendly SEO)

Pourquoi ça compte ?
C'est-à-dire
- Oui. Qu'est-ce que le problème demande?
Formules et mathématiques derrière Mots clés Formules de conversion de température
Solutions spécifiques à la langue
Cases et tests de bord
Analyse de complexité
Conseils d'entrevues
Ressources et lectures complémentaires Autres

- Oui. Exemple de structure de blog

```markdown
# Convertir la température – LeetCode 2469 Expliquée (Java, Python, C++)

Résumé du problème
...

Formules mathématiques et conversion
...

Solution Java 0-ms
"Java
solution de classe publique { ... }
«» "

Solution Python 0-ms
'`python
Solution: ...
«» "

C++ 0-ms Solution
'`cpp
solution de classe { ... }
«» "

## Couverture et stratégie d'essai
...

Complexité et performance
...

Conseils pour l'entrevue
...

Ressources supplémentaires
...
«» "

Liste des mots clés (pour référencement)

- Convertir la température
- LeetCode 2469
- Formules de conversion de température
- Entretien de codage Java
- Entretien de codage Python
- Entretien de codage C++
- O(1) complexité temporelle
- Problème de codage des entretiens
- Préparation de l'entretien technique
- Entretien d'emploi en génie logiciel

Crochet de fermeture

> En maîtrisant ce problème apparemment trivial, vous montrez aux intervieweurs que vous pouvez écrire un code propre et efficace qui gère la précision des points flottants, une compétence critique pour tout moteur ou ingénieur système. Continuez à pratiquer et à partager vos solutions sur GitHub – votre prochaine entrevue pourrait être juste une demande de retrait! (en milliers de dollars)

---

Comment cela aide votre travail de chasse

1. **Showcase Clean Code** – Vos solutions n'utilisent que l'essentiel, prouvant que vous pouvez écrire un code maintenable.
2. **Démontrer la vitesse de résolution des problèmes** – 0 ms en Java, Python et C++ signifie que vous pouvez le résoudre en moins d'une seconde.
3. **Discipline de mise à l'essai** – Le tableau de cas de bord montre que vous considérez la robustesse.
4. **Construisez un portfolio** – Ajoutez la solution et l'article de blog à votre GitHub/LinkedIn. Les recruteurs aiment les candidats qui expliquent leur processus de pensée.

> * Conseil professionnel :* Après l'affichage, ajoutez une section de commentaires où vous répondez à des questions comme : Pourquoi utiliser `double` au lieu de `float`? Cela montre la profondeur et la disponibilité à s'engager.

---

Les pensées finales

Convertir la température peut sembler simple, mais c'est une vitrine parfaite de codage propre et efficace**. En le maîtrisant en plusieurs langues et en l'expliquant dans un blog SEO-friendly, vous ne vous préparez pas seulement à l'entrevue, mais créez aussi du contenu qui peut vous aider à vous démarquer des recruteurs. Bonne chance, et continuez à coder ! C'est ce qu'il a dit.

---