---
titre: LeetCode 2651. Calculer l'heure d'arrivée différée -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 2651 – Calculer l'heure d'arrivée différée
**Numéro de code:** 2651. Facile **Catégorie:** Mathématiques

> **Problème** – Compte tenu d'un "heure d'arrivée" (0 ≤ arrivée < 24) et d'un "temps différé" (1 ≤ temps différé ≤ 24) en heures, retourner l'heure (0 – 23) à laquelle le train arrivera finalement.
> **L'heure est exprimée en 24 heures**.

> **Exemple**
> `` "
> arrivéeHeure = 13, retardHeure = 11 → (13 + 11) % 24 = 0
> `` "

La solution est une seule opération arithmétique et est donc O(1) dans le temps et l'espace.

---

Code – Trois langues

Langue Code Complexité Notes
- C'est quoi ?
**Java**= [Voir ci-dessous](#java)=1 heure O(1), espace O(1)=Utilisez `% 24` pour l'enroulement. Autres
**Python**= [Voir ci-dessous](#python)=1 heure O(1), espace O(1)=Modulo travaille sur des entiers. Autres
**C++**= [Voir ci-dessous](#cpp)==1 heure, O(1) espace==1 arithmétique `int`; aucun risque de débordement. Autres

---

### <a name="java"></a>Java

"Java
// 2651. Calculer l'heure d'arrivée différée – Java
// O(1) temps, O(1) espace

solution de classe publique {
public int findDelayedArrivalTime(int arrivalTime, int différéTime) {
// Résumez les temps et enroulez après 24 heures
retour (arrivée et retard) % 24;
}

// Méthode principale optionnelle pour les tests manuels rapides
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Système.out.println(s.findDelayedArrivalTime(15, 5)); // 20
Système.out.println(s.findDelayedArrivéeHeure(13, 11)); // 0
}
}
«» "

---

### <un nom="python"></a> Python

'`python
# 2651. Calculer l'heure d'arrivée différée – Python
Temps O(1), espace O(1)

Solution de classe:
def findDelayedArrivée Heure(même, arrivéeHeure: int, différéHeure: int) -> Int:
retour (arrivée et retard) % 24


Essais rapides
si __nom__ == "__main__" :
s = Solution()
print(s.findDelayedArrivéeHeure(15, 5) # 20
date d'arrivée(13, 11)) # 0
«» "

---

### <a name="cpp"></a>C++

'`cpp
// 2651. Calculer l'heure d'arrivée différée – C++
// O(1) temps, O(1) espace

solution de classe {
public:
int findDelayedArrivalTime(int arrivageTime, int delayTime) {
retour (arrivée et retard) % 24;
}
};

Int main() {
Solution s;
temps d'arrivée (15, 5) << '\n'; // 20
md::tout << s.findDelayedArrivéeHeure(13, 11) << '\n'; // 0
}
«» "

---

Les bons, les mauvais et les affreux

Comment le corriger
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bonne**) • O(1) arithmétique → rapide dans l'entrevue<br>• Pas de boucles ou de structures de données → code minimal<br>• La manipulation de cas de bord (`24 → 0`) montre la compréhension du modulo
**Le problème peut sembler trivial, mais il peut aller à l'encontre des gens qui oublient l'enveloppement<br>• La suringénierie avec les boucles ou le formatage de la chaîne peut conduire à des bogues inutiles. • Écriture `arrivéeTime + retardTime` et oubli `% 24` Autres
• L'utilisation d'instructions `if` pour chaque heure (0–23) est une odeur de code<br>• Ignorer la contrainte `délayedTime <= 24` conduit à un débordement potentiel dans d'autres langues (pas un problème ici) Autres

---

- Oui. Pourquoi ce problème a-t-il des répercussions sur les entrevues?

1. ** Pensée mathématique** – L'idée de base est de reconnaître que le temps "wraps" après 24 heures. Ceci teste la capacité d'un candidat à cartographier un scénario réel à une simple formule arithmétique.

2. **Constant-Time Brilliance** – Les intervieweurs aiment les solutions O(1) parce qu'elles démontrent un processus de pensée propre et optimal.

3. **Connaissance des cas** – L'astuce cachée est l'enroulement; de nombreux candidats supposent silencieusement que l'addition de 24 heures reste toujours < 24. Une réponse solide doit explicitement gérer la frontière.

4. **Maîtrise de la langue brute** – La même logique se traduit par Java, Python et C++. Afficher la même solution concise en plusieurs langues est un grand rappel de CV.

---

Article de blog optimisé du SEO

> **Titre**: *Code à gauche 2651 – Calculer l'heure d'arrivée différée : Solutions Java, Python & C++ + Interview Insight*
> **Meta Description**: Master LeetCode 2651 avec le code clair Java, Python et C++, apprendre la complexité du temps, et obtenir des conseils d'entrevue pour impressionner les recruteurs.

---

Introduction

Si vous préparez une entrevue d'ingénierie logicielle, vous rencontrerez bientôt *LeetCode 2651 – Calculez l'heure d'arrivée différée*. C'est un problème faussement simple qui teste votre capacité à raisonner environ 24 heures d'enroulement et votre maîtrise de l'arithmétique de base en code. Ci-dessous, vous trouverez **des solutions propres, prêtes à la production** dans **Java, Python et C++**, ainsi qu'une analyse de style interview du *bon, du mauvais et du laid*.

---

Récapitulation des problèmes

On vous donne deux entiers :

Variable Gamme de signification
C'est quoi ?
Heure d'arrivée 0 – 23 heures
Temps différé 1 – 24 heures supplémentaires de retard

Retournez l'heure (0 à 23) quand le train arrivera finalement. Au format 24 heures, 24 est représenté par « 0 ».

**Exemple**

Texte
temps d'arrivée = 13, temps retardé = 11
Résultat = (13 + 11) % 24 = 0 // 00:00
«» "

---

### # # Une perspective fondamentale

L'opération **seulement** nécessaire est **addition suivie d'un module 24**. Cela garantit que tout débordement au-delà de 23 enveloppe autour au début du lendemain.

---

Solutions

C'est vrai. Java

"Java
solution de classe publique {
public int findDelayedArrivalTime(int arrivalTime, int différéTime) {
retour (arrivée et retard) % 24;
}
}
«» "

Python

'`python
Solution de classe:
def findDelayedArrivée Heure(même, arrivéeHeure: int, différéHeure: int) -> Int:
retour (arrivée et retard) % 24
«» "

C++

'`cpp
solution de classe {
public:
int findDelayedArrivalTime(int arrivageTime, int delayTime) {
retour (arrivée et retard) % 24;
}
};
«» "

Les trois solutions fonctionnent dans **O(1) time** et **O(1) space**.

---

Les bonnes

- **Simplicité** – Une ligne de code plus une méthode d'emballage.
- **Optimalité** – Temps et espace constants.
- **Réflexion claire** – Facile à expliquer dans une entrevue.

Les mauvais

- **Oubli commun** – L'omission du module conduit à des réponses erronées pour des entrées comme `arrivéeTime = 20, retardTime = 5`.
- **Suringénierie** – Ajouter des boucles ou des chaînes de formatage gonfle la solution.

La moche

- **Vérifications codées en dur** – L'écriture d'un bloc "si" pour chaque heure est un cauchemar d'entretien.
- **Wong retour type** – Retour `"20:00"` comme une chaîne lorsque la spécification nécessite un entier.

---

Conseils d'entrevue

1. **Énoncer la case de bord** – Nous devons nous envelopper après 23, donc nous prendrons la somme modulo 24.
2. ** Contraintes de la Mention** – Parce que `délayedTime` ≤ 24, le débordement entier n'est pas un problème dans ces langues. (en milliers de dollars)
3. **Montrer la solution** – Écrivez la ligne unique et soulignez son élégance.
4. **Demander des éclaircissements** – On doit gérer des minutes ? Devrait-on retourner comme 0 ? (en milliers de dollars)

---

À emporter

LeetCode 2651 est un problème classique qui récompense des solutions propres et à temps constant. En maîtrisant ce problème dans **Java, Python et C++**, vous démontrez :

- Compétences interculturelles
- Attention aux cas bord
- Capacité de produire des solutions de production et de code minimal

Insérez-le sur votre CV avec une brève balle :
> *Solved LeetCode 2651 (=Calculer l'heure d'arrivée différée=) en Java, Python et C++ – O(1) solution temps et espace en utilisant modulo arithmétique. *

Bonne chance dans vos interviews – maintenant vous êtes prêt à parler du temps, modulo, et l'art d'écrire un code élégant!