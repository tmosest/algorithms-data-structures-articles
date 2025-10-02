---
titre: LeetCode 878. Nth Magical Number -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 878. Nth Magical Number – Une plongée profonde avec Java, Python & C++ Solutions

> **TL;DR**
> Le problème Nth Magical Number est résolu dans **O(log n)** time par recherche binaire sur la plage de réponses et en utilisant le principe inclusion-exclusion avec LCM.
> Des extraits de code dans **Java, Python et C++** sont fournis.
> Un billet de blog complet suit qui explique l'astuce, les pièges (-) (-), les meilleures pratiques (-) et pourquoi cette solution impressionnera les gestionnaires d'embauche.

---

## -Déclaration de problème (Code de débit 878)

Un nombre *magical* est un entier positif divisible par **a** ou **b**.
Avec trois entiers **n, a, b**, retourner le nombre magique *nth*.
Parce que la réponse peut être énorme, le rendre modulo `109 + 7`.

**Contrôles* *

- Oui.
-- -- -- -- -- --
"1 ≤ n ≤ 109" "2 ≤ a, b ≤ 4·104" Autres

---

Remarques clés

1. **Compte des nombres divisibles**
Pour un `x` donné, le nombre de nombres ≤ `x` divisible par `a` est `x / a`.
De même pour `b` et `lcm(a, b)`.

2. **Inclusion–Exclusion**
`cnt(x) = x/a + x/b – x/lcm(a, b)`
donne le nombre de nombres magiques ≤ `x`.

3. **Recherche binaire sur la réponse**
Nous avons besoin du plus petit `x` tel que `cnt(x) ≥ n`.
La portée de recherche est `[min(a,b), n *min(a,b)]`.
Cela garantit que la réponse est dans la plage.

4. **Dépassement et Modulo**
Utilisez l'arithmétique 64 bits pour les résultats intermédiaires (LCM, multiplication).
Enfin, retourner «réponse % (109 + 7)».

---

Aperçu de l'algorithme

1. ** Calculer le GCD** de `a` et `b` (Euclid).
2. Calculer `lcm = a / gcd * b` (utiliser 64 bits pour éviter le débordement).
3. Recherche binaire sur `[low, high]`:
- "mid = (faible + élevé) / 2`
- Si `cnt(mid) < n` → rechercher la moitié droite (`faible = milieu + 1`)
- Sinon → chercher la moitié gauche (`haut = milieu`).
4. Le résultat est `low` (ou `high`), modulo `MOD = 1_000_000_007`.

---

Mise en œuvre

Voici des implémentations propres et autonomes dans **Java, Python et C++**.
Chaque programme définit une classe `Solution` (Java & C++) ou une fonction `nthMagicalNumber` (Python) qui peut être déposée directement dans une soumission LeetCode.

---

### Java

"Java
solution de classe {
finale statique privée longue MOD = 1_000_000_007L;

public int nthMagicalNumber(int n, int a, int b) {
long A = a, B = b;

// 1. Calculer le MCV
long gcd = gcd(A, B);
long lcm = (A / gcd) * B; // 64-bit

// 2. Limites de recherche binaire
long bas = Math.min(a, b);
longueur élevée = faible * (long) n; // limite supérieure sûre

pendant que (faible < haut) {
long milieu = faible + (élevé - faible) / 2;
long cnt = milieu / a + milieu / b - milieu / lcm;

si (cnt < n) {
faible = milieu + 1;
} autre {
haute = moyenne;
}
}
retour (int) (faible % MOD);
}

privé long gcd(long x, long y) {
pendant que (y != 0) {
long t = x % y;
x = y;
y = t;
}
retour x;
}
}
«» "

---

Python

'`python
Solution de classe:
MOD = 1 000 000 007

def nthMagicalNumber(self, n: int, a: int, b: int) -> Int:
d'importation de mathématiques gcd

lcm = a // gcd(a, b) * b

faible, élevée = min(a, b), min(a, b) * n

alors que faible < élevé:
milieu = (faible + élevé) // 2
cnt = milieu // a + milieu // b - milieu // lcm
si cnt < n:
faible = milieu + 1
Sinon:
haute = moyenne

retour faible % de soi. MOD
«» "

---

C++

'`cpp
solution de classe {
public:
longue MOD = 1'000'000'007LL;

long long gcd(long long a, long b) {
pendant que b) {
long t = a % b;
a = b; b = t;
}
retour a;
}

nthMagicalNumber(int n, int a, int b) {
long lcm = (long long)a / gcd(a, b) * b;

longue basse longue = min(a, b);
long long haut = faible * 1LL * n; // lien supérieur

pendant que (faible < haut) {
long moyen = faible + (élevé - faible) / 2;
long long cnt = milieu / a + milieu / b - milieu / lcm;
si (cnt < n) faible = milieu + 1;
Autre haut = milieu;
}

retour (int)(faible % MOD);
}
};
«» "

---

Les bons, les mauvais et les méchants

Aspect Explication
C'est pas vrai.
**Bonne**** • **O(log n)** temps, bien meilleur que la force brute (O(n)). <br>• Utilise l'arithmétique 64 bits pour éviter les débordements. <br>• Poigne le modulo proprement à l'extrémité. <br>• Les limites de recherche binaire sont mathématiquement prouvées pour contenir la réponse. Autres
**Bad** Si vous oubliez de lancer à 64 bits (Java `long`, aide aux ints arbitraires de Python, C++ `long`), vous risquez de déborder en calculant `lcm` ou `mid`. <br>• Erreurs hors-par-un dans les limites de recherche binaire (utiliser `low < high` et `mid = low + (high - low) / 2`). Autres
L'étape d'inclusion-exclusion ('cnt = milieu/a + milieu/b - milieu/lcm') semble simple mais peut être une source de bugs subtils si `lcm` est zéro (pas possible ici mais bon à garder). <br>• Le calcul GCD/LCD peut être sur-utilisé pour les débutants; un «gcd = std::gcd(a, b)» en C++17 aide. <br>• Rappelez-vous que la réponse doit être retournée modulo `109+7`; oublier cela peut causer une mauvaise réponse sur d'énormes cas de test. Autres

---

Analyse de complexité

Opération Temps Espace
- C'est quoi ?
GCD/LCM. Autres
Recherche binaire "O(log(n * min(a,b))" Autres
Total "O(log n)" "O(1)" Autres

L'empreinte mémoire est constante – aucun tableau supplémentaire ou récursion.

---

Cas d'essai

"n"
C'est quoi ?
Dénomination des marchandises
C'est la première fois que l'on s'en occupe.
C'est vrai.
1999999998 (mod 109+7)
100 000 400 000 400 000

Exécutez chaque extrait dans l'environnement de sa langue ou sur le panneau « Code de course » de LeetCode.

---

Conclusion optimale du SEO

Si vous préparez des entrevues d'ingénierie logicielle, la maîtrise du problème **Nth Magical Number** démontre :

1. **La pensée algorithmique** – reconnaître la nécessité d'une recherche binaire sur l'espace de réponse.
2. **Rigeur mathématique** – application de l'inclusion – exclusion, GCD, LCM.
3. **Codage Discipline** – traiter les grands nombres, en utilisant l'arithmétique 64 bits, et les opérations modulo correctement.

Utilisez les extraits de code ci-dessus dans votre portfolio ou GitHub README pour mettre en valeur votre compétence. La structure de l'article de blog – énoncé de problème, observations clés, algorithme, code, complexité – s'harmonise avec ce que les recruteurs recherchent dans *explications de la solution LeetCode*.

**Mots clés** qui stimuleront votre référencement :
`LeetCode 878`, `Nth Magical Number`, `binary search`, `LCM`, `GCD`, `coding interview`, `algorithmic problem resolution`, `O(log n)`, `Java solution`, `Python solution`, `C++ solution`, `interview preparation`.

Partagez cet article sur Medium, Dev.to, ou votre blog personnel, ajoutez des balises pertinentes, et vous serez sur le radar des gestionnaires d'embauche à la recherche de candidats qui peuvent transformer les mathématiques en code efficace.

Joyeux codage – et que Nth numéro magique soit toujours à quelques lignes!