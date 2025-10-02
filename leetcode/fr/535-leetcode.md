---
titre: LeetCode 535. Encoder et décoder TinyURL - Oui.
description: Titulaire
Date: 2025-09-21
catégories: []
auteur: Moses
étiquettes: []
hideToc : vrai
---
535. Encoder et décoder TinyURL – Code, Concepts & SEO-Ready Blog

> **Cible du faisceau de mots clés :** *Encoder et décoder TinyURL, raccourcisseur d'URL TinyURL, LeetCode 535, codage d'entretien d'emploi, solution Java/Python/C++, encodeur d'URL, entretien d'ingénierie logicielle. *
> **Titre (SEO):** Encoder et décoder TinyURL (LeetCode 535) – Java, Python & C++ Solutions

---

Résumé du problème (Code de bord 535)

> **Objectif:** Concevoir un service d'URL minuscule – `encode(longUrl)` retourne une URL raccourcie; `decode(shortUrl)` retourne l'URL longue d'origine.
> **Contreparties :**
> * `1 ≤ longueur de l'url ≤ 104 "
> * Le même objet `Codec` est utilisé pour les deux encode/décode; aucune garantie de collisions.
> * Vous pouvez choisir n'importe quel schéma d'encodage – chaînes base‐62, hachage, compteur, etc.

> **Pourquoi ça compte :** Les raccourcisseurs d'URL sont partout (TinyURL, Bit.ly, GitHub Gists). Les intervieweurs aiment ce problème parce qu'il teste:
> * Utilisation de Hashing & dictionnaire
> * Aléatoire & prévention des collisions
> * compromis espace/temps
> * Conception pratique d'API

---

Approches de conception communes

Une approche pour les avantages pour les consommateurs
-- -- -- -- -- -- -- -- -- -- -- --
**Random 6‐char base‐62 + HashMap**=• Extrêmement simple <br>• Opérations à temps constant <br>• Facile à réinitialiser==• Besoins de vérification de collision (rare) <br>• Non déterministe==LeetCode & services à petite échelle===
Autres 2.00 **Comptoir incrémental + base-62**.00 • Pas de collisions, déterministe <br>• URLs prévisibles.00 • État de persistance requis <br>• URLs plus longues si de nombreuses entrées.
* Pas de stockage nécessaire (pur apatride) <br>• Rapide • Chocs possibles <br>• Le hachage tronqué peut se briser
Autres Encodage personnalisé (base‐36, base‐64, ou Huffman)

> **À retenir :** Pour le codage des entrevues, l'approche 6-char base-62* (approche 1) est la norme de facto. Il équilibre la simplicité, la justesse et le raisonnement clair.

---

- Oui. Solutions de référence

> **Note:** Toutes les solutions sont autonomes, utilisent `HashMap`/`dict`/`unordered_map`, et maintiennent l'état dans une seule classe.

#### 3.1 Java (style OOP)

"Java
Importer java.util. HashMap;
Importer java.util. Aléatoire;

Classe publique Codec {
chaîne statique privée ALPHABET = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
interne statique privée CODE_LEN = 6;

final privé Random aléatoire = nouveau Random();
HashMap<String, String> carte = nouvelle HashMap<>();

/** Générer une clé aléatoire de 6 caractères */
chaîne privée générerKey() {
StringBuilder sb = nouveau StringBuilder(CODE_LEN);
pour (int i = 0; i < CODE_LEN; i++) {
sb.append(ALPHABET.charÀ(random.nextInt(ALPHABET.longueur())));
}
retour sb.toString();
}

/** Encode une URL vers une URL raccourcie. */
chaîne publique encode(String longUrl) {
Clé de chaîne;
Faites {
clé = generateKey();
} pendant que (map.contientKey(key)); // Éviter les collisions
map.put(key, longUrl);
retour "http://tinyurl.com/" + clé;
}

*** Décode une URL abrégée à son URL originale. */
décode de chaîne publique(Short de chaîne) {
Clé de chaîne = shortUrl.replace("http://tinyurl.com/", "");
retour map.get(key); // Garantie d'existence
}
}
«» "

> **Complexité**
> *Heure:* "O(1)" moyenne pour les deux "encode" et "décode".
> *Espace:* `O(N)` où `N` est le nombre d'URL encodées.

---

3.2 Python

'`python
importation aléatoire
importer la chaîne

classe Codec:
_ALPHABET = chaîne. chiffres + string.ascii_lettres
_CODE_LEN = 6

def _init_(self):
auto._store = {}

def _random_code(self) -> str:
retourner ''.join(random.choice(self._ALPHABET) pour _ in range(self._CODE_LEN))

def encode(self, long_url: str) -> str:
alors que Vrai:
code = auto_code_random()
si le code n'est pas dans Self._store: # Contrôle de collision
pause
Self._store[code] = long_url
retourner f"http://tinyurl.com/{code}"

def décode(self, short_url: str) -> str:
code = short_url.replace("http://tinyurl.com/", "")
retourner self._store[code]
«» "

> ** Touches pyroniques* *
> * `string.digits + string.ascii_letters` donne l'alphabet base-62.
> * `self._store` est le dictionnaire interne.

---

### 3.3 C++

'`cpp
#inclut <non-ordonné_map>
#incluez <string>
#incluez <random>

Codec {
l'alphabet "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
code d'entrée du constexpr statiqueLen = 6;

std::unordered_map<std::string, std::string> mp;
md::mt19937 rng{ std::random_device{}()};
L'analyse de l'incidence de l'effet de serre sur la santé est fondée sur les données suivantes: dist{0, 61};

std::string randCode() {
std::chaîne s(codeLen, '\0');
pour (int i = 0; i < codeLen; ++i) {
s[i] = alphabet[dist(rng)];
}
retour s;
}

public:
md::string encode(const std::string& longUrl) {
md:: touche de chaîne;
Faites {
clé = randCode();
} pendant (mp.find(key) != mp.end()); // contrôle de collision
mp[key] = longue — d'une part, et
retour "http://tinyurl.com/" + clé;
}

(suite)
md::clé de chaîne = shortUrl.substr( shortUrl.find_last_of('/') + 1);
retour mp[key]; // garanti pour exister
}
};
«» "

> **Pourquoi `mt19937`?**
> Il s'agit d'un PRNG rapide et de haute qualité adapté au codage des entretiens et des services réels.

---

- Oui. Les bons, les mauvais et les méchants

La catégorie La bonne La mauvaise La mauvaise
- C'est quoi ?
**Simplicité**= Les clés aléatoires 6-char sont *tiny* et faciles à mettre en œuvre. Il faut gérer de rares collisions. Une sur-ingénierie (p. ex., verrouillage distribué, ardeur) pour une entrevue simple. Autres
**Déterminisme** Les solutions aléatoires produisent des URL différentes chaque exécution → pas idéal pour les tests unitaires. L'utilisation de l'état RNG statique global peut conduire à des tests flous. Autres
**Scalabilité**=HashMap fonctionne bien pour des millions d'URL en mémoire. La mémoire grandit linéairement; elle ne persiste pas. Autres
**Sécurité**=Les URLs courtes et non-visables protègent contre le dénombrement. Les cordes aléatoires peuvent encore être forcées à grande échelle. L'exposition de la cartographie (par exemple, au moyen d'impressions de débogage) fuit les données. Autres
**Thread‐Safety**=Java's `HashMap` est *pas* thread‐safe; Python=s dict n'est pas non plus thread‐safe. Ignorer la concurrence peut causer des conditions de course. Dans un vrai petit serviceURL, vous devriez verrouiller ou utiliser `ConcurrentHashMap`. Autres
**Les préoccupations du monde réel** Les collisions aléatoires nécessitent une logique de régénération. L'utilisation de services externes (Redis, S3) pour la persistance ajoute la latence et la complexité. Autres

---

C'est pas vrai. Optimisations et variantes

Idées de mise en œuvre
- C'est quoi ?
**Comptoir de base‐62**= Conversion d'un compteur entier en chaîne de base‐62. URL déterministe, plus facile de débogage. Autres
Utiliser `hashlib.sha256(longUrl)` → prendre les 6 premiers octets. Service apatride; stockage minimal. Autres
**Préfixe avec domaine**=Enregistrez le domaine dans un fichier de configuration, par exemple `http://tinyurl.com`.= Flexible pour plusieurs locataires. Autres
**Clés plus courts**= Utiliser les clés 4-char → 624=14 millions de combos uniques.= Si vous connaissez votre URL < 14M. Autres
**Apatrides**= Retour `https://tinyurl.com/` + base62(sha256(longUrl)=" Pas de stockage, pas de carte de décodage (mais perdre la recherche inverse). Autres

---

## 6-

1. ** Préciser d'abord les prescriptions* *
* Demandez si la persistance est nécessaire.
* Êtes-vous autorisé à utiliser des bibliothèques externes?
* Et la sécurité des fils?

2. **Exposer les compromis de conception**
* Random vs contre hash.
* Stratégie de gestion des collisions.

3. **Écrire un code propre**
* Préoccupations distinctes : génération de clés, gestion des cartes.
* Utilisez des constantes pour le domaine, l'alphabet, la longueur de la clé.

4. **Discussion des cas de bord**
* URLs très longues (10 kB).
* Réencodage de la même URL plusieurs fois.

5. **Afficher la complexité**
* Temps `O(1)`, espace `O(N)`.
* Potentiel de blocage de la mémoire pour l'énorme N.

6. **Offre une extension de production**
* Persistez la carte dans un DB.
* Utilisez un compteur distribué.
* Ajouter la limitation des taux et l'analyse.

---

Les pensées finales

- Oui. La solution *random 6-char base‐62* est la réponse du manuel pour LeetCode 535 – elle équilibre la brièveté, la justesse et la performance.
- Oui. Dans un vrai service, vous vous êtes penché vers une approche **contre-basée** avec stockage persistant (p. ex. Redis) pour garantir l'unicité et permettre l'analyse.
- Gardez toujours la portée de l'entrevue à l'esprit : montrez que vous comprenez les compromis, pouvez écrire un code propre et pouvez discuter d'extensions potentielles du monde réel.

> **Astuce pro pour la chasse au travail** – postez ces solutions sur votre repo GitHub, marquez-les avec `tinyurl`, et mentionnez-les dans votre curriculum vitæ. Les recruteurs aiment voir l'implémentation exacte que vous avez utilisée pour un problème d'entrevue classique.

---

Vous voulez plus de pratique ?

- **Problèmes de codage de l'entrevue** – plus de 30 questions portant sur les structures de données, les algorithmes et la conception du système.
- **Répertoire GitHub** – `tinyurl-leetcode-535` avec toutes les variantes linguistiques et les tests unitaires.
- **Séance de codage en direct** – organiser une entrevue simulée d'une heure sur GMeet ou Zoom; je vais vous guider dans ces solutions.

> ** Préparez-vous**: Vous venez de maîtriser l'une des questions d'entrevue les plus courantes. Utilisez les idées ci-dessus pour as la prochaine interview technique!

---

- Oui. **SEO Mots-clés**: conception TinyURL, solution LeetCode 535, cartographie aléatoire de base‐62, raccourcissement de l'URL, entretien de la carte de hachage, raccourcisseur de l'URL contre-basé, évitement de collision, service de minusculeURL du monde réel, patrons d'entrevue de codage.

---

Bonne chance 