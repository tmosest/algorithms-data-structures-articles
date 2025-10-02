---
titre: LeetCode 1344. Angle entre Les mains d'une horloge -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Code – 3 langues

Voici des solutions propres et prêtes à coller pour LeetCode **1344 – Angle entre les mains d'une horloge**.
Chaque implémentation suit le même **méthode unitaire** et est écrite dans un style facile à lire, à tester et à discuter dans une entrevue.

---

#### 1.1 Java

"Java
***
* 1344. Angle entre les mains d'une horloge
*
* Le problème peut être résolu avec une seule ligne de maths:
* angle horaire = (heure % 12) * 30 + minutes * 0,5
* angle des minutes = minutes * 6
* différence = abs (angle horaire - angle minute)
* réponse = min(différence, 360 - différence)
*
* Complexité temporelle : O(1)
* Complexité spatiale: O(1)
*/
solution de classe {
double angle publicClock(int heure, minutes int) {
// 1 heure == 30 degrés, 1 minute == 0,5 degrés pour la main d'heure
double heure Angle = (heure % 12) * 30,0 + minutes * 0,5;

// 1 minute == 6 degrés pour la main minute
double minute Angle = minutes * 6,0;

// Prendre l'angle plus petit
double diff = Math.abs(heureAngle - minuteAngle);
retourner Math.min(diff, 360.0 - diff);
}
}
«» "

---

#### 1.2 Python

'`python
# 1344. Angle entre les mains d'une horloge
Temps: O(1), Espace: O(1)

Solution de classe:
angle de défi Horloge(même, heure: int, minutes: int) -> flotteur:
_angle horaire = (heure % 12) * 30 + minutes * 0,5
_angle de minute = minutes * 6
diff = abs(heure_angle - minute_angle)
retour min(diff, 360 - diff)
«» "

---

*## 1.3 C++

'`cpp
/* 1344. Angle entre les mains d'une horloge
* O(1) temps, O(1) espace
*/
solution de classe {
public:
double angleClock(int heure, minutes int) {
double heure Angle = (heure % 12) * 30,0 + minutes * 0,5;
double minute Angle = minutes * 6,0;
double diff = std::abs(heureAngle - minuteAngle);
retour std::min(diff, 360.0 - diff);
}
};
«» "

---

- Oui. 2. Article de blog – Le bon, le mauvais et le mauvais de LeetCode 1344

> *Les angles de l'horloge de maîtrise: un guide complet du code de leet 1344 – Des bases à l'entrevue – Code de préparation*

2.1 Pourquoi ce problème compte

- **Question d'interview classique** – il montre que vous pouvez mélanger la géométrie avec l'arithmétique.
- ** Léger mais intelligent** – seulement 1 ligne de maths; une vitrine parfaite de codage propre.
- **Testing Edge Cases** – vous force à gérer l'enroulement de 12 heures et le flip de 360 degrés évident.

2.2 Récapitulation du problème

> **Input**: `heure (1...12)`, `minutes (0...59)`
> ** Sortie**: L'angle plus petit (en degrés) entre les aiguilles d'heure et de minute, précis à `10−5`.

2.3 Les bonnes – Maths simples

Concept Valeur
C'est quoi ?
Autres L'heure bouge à la main 30° par heure
Autres L'heure bouge à la main 0,5° par minute
Les mouvements de la main dans les minutes 6° par minute

**Formule* *

«» "
= (heure % 12) * 30 + minutes * 0,5
minute Angle = minutes * 6
différence ===HourAngle - minuteAngle==
réponse = min(différence, 360 - différence)
«» "

- `heure % 12` gère le boîtier de bord de 12 degrés.
- `min(différence, 360 - différence)` choisit automatiquement l'angle plus petit.

2.4 Les mauvaises – Pièges communs

Pourquoi il casse
C'est pas vrai.
Oubliant `% 12`
Autres Division entière (en anglais seulement) `minutes / 60` devient 0 en Java/C++. Autres
Autres Ne prenant pas la différence absolue Autres
Autres Différence brute de retour > 180: mauvais angle plus petit `min(diff, 360 - diff)` Autres
Erreurs d'arrondi du point flottant

2.5 La suringénierie

C'est tentant d'écrire une simulation "étape par étape" :

Texte
pour chaque minute:
déplacer l'heure main de 0,5°
déplacer la main minute par 6°
«» "

Mais cela ajoute des boucles, de l'état et une complexité inutile. La solution de "gugly" ressemble souvent à:

"Java
// Trop de variables, nombres magiques et contrôles redondants
«» "

**Règle du pouce** – garder la solution **indépendante** et **basée sur la formule**. La simplicité est un signe de bonne résolution de problèmes.

2.6 Optimisation des entrevues

1. ** Expliquez les mathématiques en amont** – montrez que vous comprenez la géométrie sous-jacente.
2. **Montrer la manipulation de cas de bord** – parler de l'astuce `12%12`.
3. **Complexité des mentions** – temps O(1), espace O(1).
4. **Ecrire le code propre** – aucune variable inutilisée, nommage cohérent.
5. ** Ajouter un cas d'essai** – par exemple `angleClock(3, 30) → 75`.

#### 2.7 SEO & Stratégie de recherche d'emploi

- **Mots-clés**: LeetCode 1344 solution, problème d'angle de l'horloge, interview de Java Python C++, problème de géométrie de O(1), meilleur code d'angle de l'horloge.
- **Méta-description**: Apprendre la solution optimale O(1) pour LeetCode 1344 – Angle entre les mains d'une horloge. Java complet, Python, C++ code + conseils d'entrevue. (en milliers de dollars)
- **Étiquettes en tête**: H1 – titre du problème; H2 – sections (bon, mauvais, mauvais, code).
- **Liens internes**: lien vers des problèmes connexes (p. ex.
- **Rich snippets**: fournir un bloc d'extrait de code pour chaque langue.
- **Engagement** : demandez aux lecteurs de commenter avec leurs propres astuces ou de partager l'article.

2.8 Réflexions finales

- Le *good* est une formule unique et élégante qui résout un problème de géométrie en O(1).
- Le *mauvais* est les nombreux pièges qui déraillent même les codeurs expérimentés; attention au modulo, division, et les erreurs de signe.
- Le *ugly* est sur-ingénierie – boucles, état ou variables supplémentaires. Gardez le poids.

Armé de cette solution et d'une explication polie, vous êtes prêt à répondre à la question d'angle d'horloge sur LeetCode et dans votre prochaine interview de codage. Bonne chance, et le codage heureux!