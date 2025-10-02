---
titre: LeetCode 2456. Créateur vidéo le plus populaire - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
- Oui. 1. Récapitulation des problèmes

> **2456 – Créateur vidéo le plus populaire**
> *Moyenne

On vous donne trois tableaux de longueur *n*:

"créateurs[i]" "ids[i]" " vues [i] " Autres
- C'est quoi ?
Créateur de la vidéo *i* id de la vidéo *i* id du nombre de vues de la vidéo *i*

La *popularité* d'un créateur est la somme des vues de toutes les vidéos de ce créateur.
Pour chaque créateur, vous devez également connaître l'identité de la vidéo **la plus vue**.
Si plusieurs vidéos se connectent pour la plupart des vues, choisissez l'id lexicographiquement plus petit.
Si plusieurs créateurs se lient pour la plus haute popularité, les rendre tous (l'ordre n'a pas d'importance).

Retourner un tableau 2-D `réponse` où chaque élément est `[créateur, id_of_best_video]`.



-----------------------------------------------------------------------------------

- Oui. 2. Algorithme (un seul passage, O(n) temps, O(n) espace)

La solution est un scan linéaire unique qui conserve une carte de hachage *simple* par créateur.

Créateur "maxVideoViews" "BestId"
- C'est quoi ?

* Total Vues` – la somme courante de toutes les vues pour ce créateur.
* `maxVideoViews` – le nombre maximum de vues vu pour toute vidéo de ce créateur.
* `bestId` – l'identifiant lexicographiquement plus petit qui a `maxVideoViews`.

**Étapes**

1. Initialiser une carte vide `mp` (`String → struct{ long total, int maxView, String bestId }`).
2. Itérer sur les 3 tableaux simultanément.
* Mettre à jour `total Vues` (ajouter les vues actuelles.
* Si `views[i] > maxVideoViews` → remplacer `maxVideoViews` et `meilleur Id'.
* Si `views[i] == maxVideoViews` → Gardez la petite identité.
3. Tandis que l'itérating garde une trace de la popularité maximale mondiale (`globalMax`).
4. Après le scan, marchez à nouveau la carte et choisissez tous les créateurs dont "total Vues == globalMax`.
Pour chacun, sortie `[créateur, bestId]`.

Parce que chaque opération sur une carte est **O(1)** en moyenne, la complexité globale est:

* **Heure** – «O(n)»
* **Espace** – `O(n)` (une entrée par créateur distinct)

L'algorithme gère les ids dupliqués naturellement parce que nous traitons chaque entrée comme une vidéo distincte.



-----------------------------------------------------------------------------------

- Oui. 3. Mise en œuvre des références

Ci-dessous vous trouverez des solutions propres et bien commentées dans les trois langues demandées.

---

#### 3.1 Java (Java 17)

"Java
Importation de java.util.*;

solution de classe publique {
// Classe d'aide pour tenir les statistiques du créateur
classe statique privée Stat {
long total Vues; // somme de toutes les vues
int maxVideoViews; // max vues d'une seule vidéo
String bestId; // lexicographiquement plus petit id parmi maxVideoViews

Stat( vues longues, chaîne id) {
Ça. Total général Vues = vues;
ce.maxVideoViews = (int) vues;
ça.meilleur Id = id;
}

mise à jour vide(vues longues, chaîne id) {
Total général Vues += vues;

si (vues > maxVideoViews) {
maxVidéoVues = (int) vues;
le meilleur Id = id;
} sinon si (vues == maxVideoViews && id.compareTo(bestId) < 0) {
le meilleur Id = id;
}
}
}

liste publique<Liste<String>> la plupart des créateurs de réseaux,
Les identificateurs,
vues int[] {
Carte <String, Stat> mp = nouveau HashMap<>();
long terme mondial Max = 0;

pour (int i = 0; i < creators.longueur; i++) {
Création de chaînes = créateurs[i];
Chaîne id = ids[i];
long v = vues[i];

mp.computeIfAbsent(créateur,
k -> nouveau Stat(v, id))
.mise à jour(v, id);

globalMax = Math.max(globalMax, mp.get(creator).totalViews);
}

Liste <Liste<String>> ans = nouvelle liste <>();
pour (entrée var : mp.entrySet()) {
if (entry.getValue().totalViews == globalMax) {
ans.add(Arrays.asList(entry.getKey(), entry.getValue().bestId));
}
}
le retour des an;
}

// Démo rapide (facultatif)
public statique vide principal(String[] args) {
Solution s = nouvelle solution();
Chaîne[] c = {"alice", "bob", "alice", "bob", "alice"};
Chaîne[] id = {"1", "2", "3", "4", "5"};
int[] v = {5, 3, 5, 2, 5};

Système.out.println(s.mostPopularCreator(c, id, v));
}
}
«» "

---

3.2 Python (Python 3,10)

'`python
de taper l'importation Liste, numéro

classe Stat:
def __init__(self, views: int, vid_id: str):
auto.total_views = vues
self.max_video = vues
Self.best_id = vid_id

def update(self, vues: int, vid_id: str) -> Aucun:
auto.total_views += vues
si vues > self.max_video:
self.max_video = vues
Self.best_id = vid_id
vues elif == self.max_video et vid_id < self.best_id:
Self.best_id = vid_id

def mostPopularCreator(créateurs: List[str], ids: List[str], vues: List[int]) -> Liste[Liste[str]]:
mp: Dict[str, Stat] = {}
global_max = 0

pour créateur, vid_id, v dans zip(créateurs, ids, vues):
si le créateur n'est pas en mp:
mp[creator] = Stat(v, vid_id)
Sinon:
mp[creator].update(v, vid_id)

global_max = max(global_max, mp[creator].total_views)

réponse: Liste[Liste[str]] = []
pour créateur, stat in mp.items():
if stat.total_views == global_max:
réponse.append([créateur, stat.best_id])

réponse de retour


♪ Démo (facultatif)
si __nom__ == "__main__" :
Créateurs = ["alice", "bob", "alice", "bob", "alice"]
ids = ["1", "2", "3", "4", "5"]
vues = [5, 3, 5, 2, 5]
print(mostPopularCreator(créateurs, ids, vues))
«» "

---

### 3.3 C++ (C++20)

'`cpp
#incluez <bits/stdc++.h>
utilisant l'espace de noms std;

// Structure qui stocke toutes les statistiques pour un créateur
struct Stat {
long total long Vues{0}; // somme de toutes les vues
int maxVideoViews{0}; // vues maximales d'une seule vidéo
meilleure chaîne Id; // plus petit id avec maxVideoViews

Stat(long long v, const string &id)
: totalViews(v), maxVideoViews(static_cast<int>(v)), bestId(id) {}

vide update(long long v, const string &id) {
Total général Vues += v;

si (v > maxVideoViews) {
maxVideoViews = static_cast<int>(v);
le meilleur Id = id;
} sinon si (v) maxVideoViews && id < best Id) {
le meilleur Id = id;
}
}
};

solution de classe {
public:
vectorielle<vector<string>> la plupartPopularCreator(vector<string> et créateurs,
vectorielle <string>&ids,
vecteur<int>& vues) {
unordered_map<string, Stat> mp;
long terme mondial Max = 0;

pour (size_t i = 0; i < creators.size(); ++i) {
const string &creator = créateurs[i];
Const string &id = ids[i];
long v = vues[i];

si (!mp.count(créateur))
mp[creator] = Stat(v, id);
Autre
mp[creator].update(v, id);

GlobalMax = max(globalMax, mp[creator].totalViews);
}

vecteur <vector<string>> ans;
pour (const auto &[creator, st] : mp) {
si (st.totalViews == globalMax) {
ans.push_back({creator, st.bestId});
}
}
le retour des an;
}
};
«» "

Les trois solutions fonctionnent en *O(n)* temps et utilisent *O(n)* espace auxiliaire – les limites optimales pour ce problème.



-----------------------------------------------------------------------------------

- Oui. 4. Bons, mauvais et mauvais – Ce que les intervieweurs En fait, je veux

Aspects Ce qui est bon Où les choses vont mal
-- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
**Bien** Un hash‐map par créateur → **O(n)** passe. <br>• Conserve *exactement* les données dont vous avez besoin : total, vidéo max et meilleur id. <br>• Poignées dupliquées automatiquement.
**Bad**) • L'utilisation de 2 à 3 cartes imbriquées (une pour la popularité, une autre pour les statistiques par id) ajoute *O(k)* espace (k = ids distincts). <br>• Vous risquez un bug subtil : ajouter les mêmes vues id=s au lieu de prendre le *maximum* d'une seule vidéo. Cela apparaît souvent dans les concours: -Je résume la même vidéo - vues deux fois. Autres
Quand plusieurs vidéos s'attachent, choisir le plus petit id nécessite une comparaison *lexicographique* – un détail minuscule mais crucial. <br>• Si vous oubliez de suivre la popularité maximale mondiale lors du premier passage, vous devrez faire un second passage de toute façon. L'histoire classique du dernier cas de test manquant – c'est généralement un cas de coin autour des liens ou de l'entrée vide. Autres

- Oui. Comment éviter les odieux

Tactique Pourquoi ça compte
-- -- -- -- -- --
**Single struct par créateur**=Conserve la logique en un seul endroit – pas de double comptage accidentel. Autres
**«computerIfAbsent» / `map.getOrDefault`**= Garantie que l'entrée de la carte n'est créée qu'une seule fois. Autres
Autres **Comparez toujours les chaînes d'id**= `id.compareTo(bestId) < 0` garantit la plus petite id pour les liens. Autres
**Track `globalMax` à la volée** Autres

Lorsque vous êtes prêt pour l'entretien, vous pouvez déposer n'importe quel code de référence dans votre dépôt de solution, ou même le transférer dans une autre langue (Rust, Go, etc.) – le même modèle s'applique.



-----------------------------------------------------------------------------------

- Oui. 5. Analyse de la complexité

Formule métrique Résultat
C'est quoi, ça ?
**Temps**="O(n)" – opérations de hachage à boucle unique, à temps constant=" **Linear**="
**L'espace**="O(m)" où *m* = nombre de créateurs distincts

Parce que *m* ≤ *n*, l'espace le plus mauvais est "O(n)".



-----------------------------------------------------------------------------------

- Oui. 6. Pourquoi ce problème est un must-Know pour votre prochaine entrevue

* **Données du monde réel** – Pensez à YouTube ou TikTok : beaucoup de créateurs, beaucoup de vidéos, d'énormes ensembles de données.
* **Carte lourde** – La plupart des développeurs seniors doivent être à l'aise avec les tables de hachage, `unordered_map`, `HashMap`, etc.
* ** Logique révolutionnaire** – Les intervieweurs aiment tester votre capacité à gérer les cas de bord et l'ordre lexical.
* ** Format de réponse multiple** – Montre que vous pouvez retourner des collections de paires, un modèle d'entrevue commun.

En maîtrisant ce problème, vous démontrez :

* **Efficacité algorithmique** (temps linéaire, mises à jour de l'espace constant).
* ** Style de codage propre** (structure de données unique, pas de boucles imbriquées).
* **Attention aux cas bord** (dupliquer les ids, les liens, les créateurs multiples).
* **Préparation à l'entrevue** – vous pouvez expliquer votre raisonnement sur le tableau blanc en moins de 5 minutes.

---

- Oui. 7. SEO–Résumé amical

- **LeetCode 2456** – * Créateur vidéo le plus populaire*
- Solution Java (HashMap, O(n) temps, O(n) espace)
- Solution Python (dictée, O(n) temps, O(n) espace)
- Solution C++ (inordered_map, temps O(n), espace O(n))
- Prép d'entrevue – expliquer les liens, la rupture des liens, le choix de la structure des données
- complexité algorithmique – temps O(n), espace O(n)
- Démo de code – rapide, propre, monopass

Si vous préparez une entrevue d'ingénierie logicielle, ajoutez cet article à votre liste d'études. Le modèle de **one map + global max** est une astuce réutilisable qui apparaît dans de nombreux problèmes de "top-k" ou "group-by" sur LeetCode et au-delà.



-----------------------------------------------------------------------------------

- Oui. 8. Prise Loin

1. **Utilisez une seule carte de hachage par créateur** – garde le code court et élimine le double comptage accidentel.
2. **Mise à jour des statistiques à la volée** – aucune seconde ne passe à travers les vidéos, un seul passe à travers les créateurs après le scan.
3. ** Méfiez-vous des liens** – gardez l'identifiant lexicographiquement plus petit chaque fois que vous touchez une situation d'égalité de vue.
4. **Testez les cas de bord** – tableaux vides, un seul créateur, tous les créateurs se lient, duplicata avec les mêmes vues, etc.

Codage heureux – et que votre prochaine entrevue passe *stream-lined* comme une vidéo à succès 