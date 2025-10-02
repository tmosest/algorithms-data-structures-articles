---
titre: LeetCode 1817. Trouver les utilisateurs Minutes actives -
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
# 1817 – Trouver les utilisateurs
*Une plongée profonde dans le problème, la solution la plus propre, et un billet de blog SEO-friendly qui peut vous poser un entretien d'emploi. *

---

- Oui. 1. Aperçu du problème

> **LeetCode 1817 – Trouver les utilisateurs Minutes actives**
> *Moyenne

On vous donne un tableau `logs` où `logs[i] = [userId, minute]` représente qu'un utilisateur a effectué une action à cette minute.
Le *User Active Minutes* (UAM) d'un utilisateur est le nombre ** de minutes distinctes** que l'utilisateur était actif.
Compte tenu d'un entier `k`, vous devez retourner un tableau 1 indexé `réponse` de taille `k` de telle sorte que `réponse[j]` est le nombre d'utilisateurs dont l'UMA est égal à «j» (pour «1 ≤ j ≤ k»).

**Contrôles* *

«» "
1 ≤ longueur des billes ≤ 10^4
0 ≤ utilisateur Id ≤ 10^9
1 ≤ minute ≤ 10^5
1 ≤ k ≤ 10^5
«» "

---

- Oui. 2. Approche directe

La solution naïve serait :

1. C'est pour chaque entrée de journal.
2. Garder une carte de l'utilisateur Id → jeu de minutes.
3. Après le traitement de tous les journaux, la taille de chaque ensemble est l'utilisateur de UAM.
4. Incrémenter le compteur dans la réponse en conséquence.

C'est exactement le modèle classique du compte unique par clé et fonctionne dans l'espace **O(n)** et **O(n)**, où `n = logs.length`.

---

- Oui. 3. Solution optimale (HashMap + HashSet)

La solution optimale suit la même idée mais avec quelques micro-optimisations :

Étape Code Pourquoi
C'est pas vrai.
"Map.computeIfAbsent(id, x -> new HashSet<>())" Évite les "conteneurs" explicites Contrôle des clés. Autres
Autres Après la construction de la carte, itérer sur `map.values()` Obtenez directement la taille de l'ensemble; pas besoin de regarder les clés à nouveau. Autres
"Réponse[setSize-1]++" "0-indexé tableau mais le problème attend 1-indexé. Autres

La complexité temporelle est **O(n)** (chaque journal traité une fois).
La complexité de l'espace est **O(n + k)** – nous stockons au plus une entrée par journal et le tableau de réponses final de la longueur `k`.

---

- Oui. 4. Edge-Case .Pièges

Un problème Pourquoi ça compte
- Oui.
Autres **Très grandes valeurs userId**.HashMap fonctionne bien, mais certaines langues peuvent être des entiers 32 bits par défaut. Utiliser `long`/`long long` si la langue par défaut est 32-bit. Autres
**Dupliquer des minutes pour un utilisateur**= Si nous oublions le jeu, les duplicatas gonflent l'UAM. Toujours utiliser un ensemble (ou dédoubler avec le tri). Autres
Le problème garantit `k` ≥ max UAM, mais si ce n'est pas le cas, il se produit un indice hors des limites. Ajouter un garde ou valider l'entrée. Autres
**Grande `k` (par exemple, 10^5) avec très peu d'utilisateurs** Ceci est inévitable pour le format de sortie requis, mais le tableau est encore léger. Autres

---

- Oui. 5. Mise en œuvre du code

Voici des solutions propres, prêtes à la production dans **Java**, **Python** et **C++**.

#### 5.1 Java

"Java
Importation de java.util.*;

solution de classe {
public int[] conclusionUtilisateursActiveMinutes(int[][] grumes, int k) {
// Carte : utilisateur Id -> Série de minutes distinctes
Carte<entier, définir<entier>>utilisateurMinutes = nouveau HashMap<>();

pour (int[] log : logs) {
id int = log[0];
int minute = log[1];
userMinutes.computeIfAbsent(id, x -> new HashSet<>())add(minute);
}

int[] response = nouvelle int[k];
pour (Set<Integer> minutes : userMinutes.values()) {
int uam = minutes.size(); // UAM pour cet utilisateur
réponse[uam - 1]++; //
}
réponse de retour;
}
}
«» "

> **Complexités**
> *Time*: `O(n)` – on passe par les journaux, on passe par les valeurs de la carte.
> *Espace*: `O(n + k)` – la carte enregistre au plus `n` entrées, la taille du tableau de réponses `k`.

---

5.2 Python

'`python
de collections importer par défautdict
de taper l'importation Liste

Solution de classe:
recherche UsersActiveMinutes(self, logs: List[List[int]], k: int) -> Liste[int]:
# user_id -> Série de minutes
minutes = par défautdict(set)

pour user_id, minute dans les journaux :
minutes[user_id].add(minute)

réponse = [0] * k
pour s en minutes.valeurs():
uam = len(s)
réponse[um - 1] += 1 # 1-indexé

réponse de retour
«» "

> **Complexités**
> *Heure*: "O(n)"
> *Espace*: 'O(n + k) "

---

C++

'`cpp
#inclut <non-ordonné_map>
#inclut <unordered_set>
#incluez <vecteur>

solution de classe {
public:
std::vector<int> findingUtilisateursActiveMinutes(std::vector<std::vector<int>& Registres, int k) {
// userId -> jeu de minutes
std::unordered_map<int, std::unordered_set<int> mp;

pour (const auto & log : logs) {
id int = log[0];
int minute = log[1];
mp[id].insert(minute);
}

(k, 0);
pour (const auto & p : mp) {
int uam = p.second.size();
si (um >= 1 && uam <= k) {
réponse[uam - 1]++; // 1-indexé
}
}
réponse de retour;
}
};
«» "

> **Complexités**
> *Heure*: "O(n)"
> *Espace*: 'O(n + k) "

---

- Oui. 6. Billet de blog: Le bon, le mauvais, et le mauvais

Titre
**LeetCode 1817: Trouver les utilisateurs des minutes actives – Une plongée profonde et une entrevue‐ Solution prête**

Description de la méta
Découvrez comment résoudre LeetCode 1817 en Java, Python et C++. Comprendre l'algorithme, les compromis entre le temps et l'espace et les pièges à éviter. Améliorez vos compétences d'entrevue de codage aujourd'hui!

Rubriques

Rubrique
C'est pas vrai.
**Définir le contexte et l'importance du problème. Autres
**Récapitulatif du problème** Autres
Autres **Observations clés** Autres
**Approche optimale**= Expliquez la solution Hashmap+set. Autres
**Analyse de la complexité** Autres
Autres **Edge-Case Gotchas** , Liste , , et , , écueils. Autres
**Exemples de code**= Fournir un code propre pour Java, Python, C++. Autres
**Conseils d'entretien**= Comment expliquer et défendre votre solution. Autres
**Conclusion** Autres

- Oui. Exemple de corps de blog

> **Introduction**
> Lors des entrevues de codage, les problèmes qui impliquent de compter des événements uniques par clé apparaissent souvent. LeetCodeS *Trouver les utilisateurs Active Minutes* (Problème 1817) est un exemple de manuel. La maîtrise ne vous permet pas seulement d'obtenir un score élevé sur LeetCode, mais démontre également aux gestionnaires d'embauche que vous comprenez l'agrégation basée sur le hash, les compromis dans l'espace temporel et les pratiques de codage robustes.

> ** Résumé des problèmes* *
> On vous donne un journal des paires `[userId, minute]`. Un utilisateur *User Active Minutes* (UAM) est le nombre de ** minutes distinctes** l'utilisateur était actif. Retourner un tableau où `réponse[j]` est le nombre d'utilisateurs dont l'UMA est égal à "j" (1-indexé).

> ** Principales observations**
> * Le crux est une déduplication de minutes par utilisateur.
> * Nous pouvons traiter chaque utilisateur indépendamment – aucune interaction entre les utilisateurs n'a d'importance.
> * Une fois que nous connaissons chaque utilisateur de l'UAM, nous nous contentons de compter les résultats.

> **Approche optimale**
> La solution canonique utilise un `HashMap` (ou `unordered_map` dans C++) qui map `userId` → `HashSet` (ou `unordered_set`) de minutes.
> * Itérer sur les logs une fois, en insérant la minute dans le jeu.
> * Après la boucle, la taille de chaque ensemble est l'utilisateur de UAM.
> * Incrémenter l'index correspondant dans le tableau de réponses (`réponse[uam-1]++`).

> ** Analyse de complexité**
> *Heure*: **O(n)** – chaque entrée de journal est traitée exactement une fois.
> *Espace*: **O(n + k)** – la carte stocke au plus une entrée par journal, et le tableau de réponses nécessite des emplacements `k`.

> **Edge-Case Gotchas**
> 1. **Dupliquer minutes** – L'oubli de l'ensemble va gonfler les comptes.
> 2. **Grand utilisateurId** – Dans les langues avec 32 bits par défaut, utilisez 64 bits entiers pour éviter les débordements.
> 3. **k < max UAM** – Le problème garantit que `k` est assez grand, mais des contrôles défensifs peuvent prévenir les accidents.

> **Échantillons de code* *
> *(Insérer Java, Python, extraits C++ de la section 5 ci-dessus)*

> **Conseils d'entrevue**
> * Commencez par décrire le choix de la structure des données et pourquoi la duplication est importante.
> * Mettre en avant la garantie de temps `O(n)` – les intervieweurs aiment les solutions linéaires.
> * Mentionnez les optimisations de mémoire potentielles (p. ex., en utilisant un «vecteur<unordered_set<int>>» si vous savez que les identifiants d'utilisateur sont denses).

> ** Conclusion**
> Le problème 1817 est trompeurment simple, mais il contient beaucoup de concepts pertinents pour l'entrevue. En écrivant la solution en Java, Python et C++, vous présenterez la polyvalence aux recruteurs à travers les piles technologiques. Pratiquez-le, prenez du temps et partagez vos résultats – vous serez un peu plus près d'obtenir ce travail de rêve.

---

- Oui. 7. Pensées finales

- Oui. L'approche **hash-map + hachage** est la solution la plus naturelle et efficace.
- Souvenez-vous toujours de l'importance de *déduplication* lors du comptage de valeurs distinctes.
- La conscience des bords vous protège des bugs qui pourraient ruiner une entrevue.
- Fournir un code propre et adapté à la langue pour impressionner les intervieweurs et les pairs.

Bon codage ! C'est ce qu'il a dit.

---

*Préparé par ChatGPT – Propulsé par OpenAI. *