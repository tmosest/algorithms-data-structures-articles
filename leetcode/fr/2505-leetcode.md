---
titre: LeetCode 2505. Ou de toutes les sommes consécutives -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Solutions de code

Voici des implémentations concises et prêtes à la production pour **LeetCode 2505 – Bitwise OU de toutes les sous-séquences** en **Java, Python et C++**.
Les trois solutions fonctionnent dans **O(n)** temps et **O(1)** espace auxiliaire – parfait pour les interviews et l'utilisation réelle.

> **Récapitulation des problèmes* *
> Avec un tableau entier `nums`, calculer
> \[
> \bigvee_{S \subseteq nums}\left(\sum_{x \in S} x\right)
> \]
> C'est-à-dire la somme bitwise OU de *chaque possible* subséquemment.

---

C++

'`cpp
// 2505. Bitwise OU de toutes les sommes consécutives
// Heure: O(n)
// Espace: O(1)
solution de classe {
public:
long subséquenceSumOr(vecteur<int>& nums) {
long an = 0; // final OU
long pref = 0; // somme du préfixe en cours d'exécution
pour (int x : nombres) {
pref += x; // somme du préfixe courant
x x x x x x x x x x
}
le retour des an;
}
};
«» "

---

### Java

"Java
// 2505. Bitwise OU de toutes les sommes consécutives
// Heure: O(n)
// Espace: O(1)
solution de classe {
public long subséquenceSumOr(int[] nums) {
long ans = 0; // final OU
longue préf = 0; //
pour (int x : nombres) {
pref += x; // somme du préfixe courant
(long) x=% pref; // inclure x et pref
}
le retour des an;
}
}
«» "

---

Python 3

'`python
# 2505. Bitwise OU de toutes les sommes consécutives
♪ Heure: O(n)
♪ Espace: O(1)
Solution de classe:
def subsequenceSumOr(self, nombres: List[int]) -> Int:
ans = 0 # final OU
pref = 0 # somme du préfixe en cours d'exécution
pour x en nombres:
pref += x
as= x= x=0 préf
retour et
«» "

> **Pourquoi cela fonctionne** –
> Chaque bit qui peut devenir `1` dans n'importe quelle somme subséquemment soit
> 1. apparaît déjà dans un élément `x`, ou
> 2. est produit par un portage à partir d'un bit inférieur quand nous additionnons un préfixe.
> Suivre le préfixe `pref` en cours d'exécution garantit que nous captons tous les porte avec un seul passage linéaire.

---

- Oui. 2. Article de blog optimisé SEO

Titre
*Cracking LeetCode 2505: Bitwise OU of All Subsequence Sums – Solutions Java, Python & C++, Intuition et Conseils d'entrevue* *

---

Description de la méta
Lutte avec LeetCode 2505 ? Apprenez la solution O(n) qui utilise une somme de préfixe en cours d'exécution, comprenez l'intuition et préparez-vous à répondre à des questions sur les opérations bitwise en Java, Python ou C++. Boostez votre CV de codage aujourd'hui!

---

2.1 Introduction

LeetCodeS** (problème #2505) est un défi *medium-level* qui teste votre compréhension de la manipulation **bitwise**, de la programmation **dynamique** et de la traversée **array**.
C'est un favori parmi les gestionnaires d'embauche chez les géants de la technologie parce qu'il force les candidats à réfléchir à la façon dont les bits se propagent par l'addition – un concept qui apparaît dans les piles d'interview **C++, Java et Python**.

Dans cet article, nous lisons:

1. Passez par les aspects **bon** du problème.
2. Révèlez les pièges **mauvais** qui font souvent monter les personnes interrogées.
3. Discutez des cas d'angle **ugly** et comment les gérer.
4. Présentez des solutions propres et prêtes à la production dans **Java**, **Python** et **C++**.
5. Partagez des questions de style interview pour approfondir votre compréhension.

> **Mots clés**: LeetCode, bitwise OR, subséquences, algorithme, O(n), interview prep, interview de codage, Java, Python, C++, interview d'emploi, CV de codage

---

## 2.2 Le bien – Pourquoi Ce problème est important

- **La pertinence du monde réel**: Les opérations bitwise sont au cœur de la programmation des systèmes, de la cryptographie et du code critique de performance.
- **Clarté conceptuelle**: Il vous force à réfléchir à la façon dont les porte-travail en ajout binaire.
- **Opposabilité en langue brute**: La même logique O(n) se traduit par Java, Python et C++, montrant une maîtrise des nuances de langage.
- ** Contraintes évolutives**: `n` jusqu'à `10^5` et `nums[i]` jusqu'à `10^9` font une solution naïve invraisemblable — testant votre capacité à concevoir des algorithmes efficaces.

---

2.3 L'erreur commune

Pourquoi ça arrive
- Oui.
**Enumeration de tous les sous-séquences**. Autres
**Utiliser `int` pour les sommes** > 231=1 Utilisez `long`/`long long` ou Python=1 des ints de précision arbitraires. Autres
**Ignorer le bit transporte** Autres
**Confuser OU avec XOR**=______________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________ Autres

---

2.4 Les cas de bord et la mise en œuvre Quirks

1. **Tous les zéros** – La réponse doit être `0`.
2. ** Grandes sommes** – Même si les chiffres individuels sont faibles, la somme courante peut atteindre `10^14' ; elle correspond toujours à 64 bits.
3. **Numéros négatifs?** – Problème garantit non-négatif, mais si vous adaptez la solution, vous devez utiliser les types signés avec soin.
4. **Très longs réseaux** – Évitez de construire des réseaux auxiliaires; la solution d'espace O(1) est essentielle.

---

## 2.5 Aperçu de l'intuition et de la preuve

1. **Définition ou définition de la notion de "bitwise"**
\[
u = \bigvee_{S} \text{sum}(S) \implie u[i] = 1 \;\text{iff}\; \exists S: \text{sum}(S)[i] = 1
\]
2. **Deux sources pour un jeu de bits**
- Le morceau est déjà présent dans un élément `x`.
- Le bit est produit par un portage à partir de bits inférieurs pendant une somme de subséquence.
3. **Les captures de somme préfixes portent* *
L'ajout de l'élément `x` actuel au préfixe `préf` en cours d'exécution tient compte de toutes les sous-séquences qui *end* à `x`.
C ' est pourquoi le document < < pref > > contient ** toutes les contributions versées** jusqu ' à ce stade.
4. ** OU tout* *
`ans= x= x=1 pref` nous assure de capturer les deux sources.
5. **Induction**
Supposons après avoir traité les premiers éléments `k-1` que la OU est correcte.
Pour l'élément `k`, nous incluons ses propres bits (`x`) et tous les bits de transport (`pref`).
Ainsi, après la mise à jour, la OU est correcte pour la première `k`.

Cet algorithme simple O(n) est à la fois optimal et élégant.

---

## 2.6 Extraits de code de préparation à la production

*(Voir la section Code en haut pour les implémentations complètes.) *

### Java (Java 11+)

"Java
solution de classe {
public long subséquenceSumOr(int[] nums) {
long ans = 0, pref = 0;
pour (int x : nombres) {
pref += x;
(long)
}
le retour des an;
}
}
«» "

Python 3

'`python
Solution de classe:
def subsequenceSumOr(self, nombres: List[int]) -> Int:
ans = pref = 0
pour x en nombres:
pref += x
as= x= x=0 préf
retour et
«» "

C++

'`cpp
solution de classe {
public:
long subséquenceSumOr(vecteur<int>& nums) {
long ans = 0, pref = 0;
pour (int x : nombres) {
pref += x;
(long)x Préf;
}
le retour des an;
}
};
«» "

---

2.7 Entretien Questions de style à pratiquer

1. **Proof** – Pourquoi `pref` capture-t-il tous les bits de transport possibles pour les sommes de subséquence?
2. **Complexité** – Si `n` étaient `10^6`, cette solution passerait-elle toujours? Expliquez.
3. **Edge cas** – Que se passerait-il si des nombres négatifs étaient autorisés?
4. **Extension** – Comment modifier l'algorithme pour renvoyer le *set* de toutes les sommes de subséquence possibles (pas seulement OR)?
5. **Alterner l'approche** – Pouvez-vous résoudre ce problème en utilisant une programmation dynamique? Comparer avec la méthode préfixe-somme.

---

2.8 A emporter et emploi Compétences prêtes

- Maîtrise de **opérations bitwise** et compréhension de leur interaction avec l'arithmétique.
- Capacité de concevoir **algorithmes linéaires, espace constant** pour les problèmes à forte contrainte.
- Traduire confortablement un algorithme entre **Java, Python et C++** – une compétence hautement souhaitable pour les rôles complets.
- raisonnement clair: capable d'expliquer *pourquoi* une solution fonctionne, ce qui est exactement ce que les gestionnaires d'embauche demandent.

---

La pensée finale

LeetCode 2505 peut sembler simple à première vue, mais c'est un problème **gateway** qui teste à la fois la profondeur conceptuelle et le codage poli. En maîtrisant l'astuce OR préfixe, vous allez non seulement répondre à ce défi, mais aussi montrer le niveau de pensée algorithmique que les entreprises de haute technologie valorisent.

Bon codage, et bonne chance pour votre prochaine interview! C'est ce qu'il a dit.

---


---


> **Auteur**: *[Votre nom]* – Ingénieur en logiciel, passionné de LeetCode, et coach de carrière pour les développeurs aspirants.
> **Personne-ressource** : `[email] Dans le GitHub "

---

**Fin de l'article**

---

Ceci complète l'ensemble de solutions complètes et le billet de blog SEO-friendly prêt à atterrir votre prochaine entrevue de codage.