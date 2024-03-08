# Variants

**Note** Toutes les expressions présentées dans le cours doivent être évaluées
dans `utop`.

## Résumé des types que l'on connait

Avant d'aller plus loin, et de découvrir une des fonctionalité les plus
importantes d'OCaml, il est utile de faire une pause et de résumer les types que
l'on connait.

Nous avons vu les types "de base":
- `bool` pour les booléens: "vrai" ou "faux".
- `int` pour les entiers: `420`, `2`, ...
- `float` pour les nombres à virgule: `4.14`, `2.0`, `3.33334`, ...
- `char` pour les caractères: `a`, `\n`, `#`
- `string` pour les chaînes de caractères: `"salut tout le monde"`, ...

Mais aussi des types pour combiner des types en des types nouveaux:
- Les types fonction: par exemple, à partir du type `int` et du type `float`, on
  a le type fonction `int -> float`. Un exemple de fonction qui a ce type ?
- Le type des listes : à partir d'un type, on peut créer le type des listes
  d'éléments de ce type. Par exemple, avec le type `float`, on peut créer le
  type des listes de nombres à virgule : `float list`.

**Est-ce que ça suffit ? Oui ? Non ?**

Non !

OCaml permet de créer des types personnalisés pour représenter ce que l'on veut
! Par exemple on pourra créer des types pour :
- Un personnage de jeu de rôle,
- Une recette de cuisine,
- Un dictionaire,
- ...

Mais avant de créer ces types, nous allons nous concentrer sur les types que
l'on connait déjà, et voir comment ils ont été défini ! Et comment nous aurions
pu les définir nous-même !

## Anatomie d'un booléen

OCaml nous permet de jeter un oeil à la définition d'un type:

```ocaml
#show bool
```

et le résultat ne se fait pas attendre!

```ocaml
type bool = false | true
```

**Mais qu'est-ce que cela peut bien vouloir dire ?**

Mais que peut bien vouloir dire :
- `type` ?
- `bool` ?
- `=` ?
- `false` ?
- `|` ?
- `true` ?

Solution:
- `type` nous indique que l'on va déclarer un type, et non autre chose (une
  valeur, un module, une pâte à tartiner, ...)
- `bool` est le nom du type,
- `false` et `true` sont les deux valeurs que peuvent prendre le type,
- `|` sert à séparer les différentes valeurs possibles.

On appelle ça un **type énuméré** : un type dont la définition énumère les
différentes valeurs possibles.

### Création d'un type énuméré

Essayons tout d'abord de recréer le type booléen :

```ocaml
type mon_bool = true | false
```
Est-ce que ça marche ? Oui !

Alors, mettons-le en français :

```ocaml
(****  NE MARCHE PAS !!!!  ****)
type mon_bool = vrai | faux
```

Pourquoi ça ne marche pas ? Pour éviter de "confondre" les "valeurs de base" des
valeurs normales, on force à utiliser des majuscules pour les nouvelles valeurs
de base.

On appelle les "valeurs de base" des **constructeurs**. Rappelez-vous ce terme !

```ocaml
type mon_bool = Vrai | Faux
```

Mais plutôt que de reprendre un type existant, ce qui n'est pas très utile,
créens-on un nouveaux !

## Du tricot en OCaml

Pour changer des stéréotypes des informaticiens, intéressons-nous au tricot.

```ocaml
type maille = Endroit | Envers
```

**Note** : Il n'y a que deux possibilités, comme pour les booléens ! On aurait
pu utiliser des booléens pour représenter ces valeurs, mais cela ne pourrait que
nous mélanger les aiguilles, et générer des bugs !

Nous pouvons maintenant utiliser ces valeurs:

```ocaml
let point_mousse = [ Endroit ]
let point_jersey = [ Endroit; Envers ]
```

Et nous pouvons aussi filter !

```ocaml
let temps_necessaire maille =
  match maille with
   | Endroit -> 1.
   | Envers -> 1.5

let retournement maille =
  match maille with
   | Endroit -> Envers
   | Envers -> Endroit
```

Augmentons un peu le type...

```ocaml
type maille =
  | Endroit
  | Envers
  | Glisse (** Passe une maille d'un côté à l'autre sans la tricoter *)
  | Jete (** "Jette" une maille *)
  | Augmente (** Crée deux mailles à partir d'une seule *)

let temps_necessaire maille =
  match maille with
   | Endroit -> 1.
   | Envers -> 1.5
```

Horreur ! Le filtrage n'est plus exhaustif ! Corrigeons cela tout de suite !

Le fait que OCaml soit capable d'emettre un warning est un très bon point pour
la maintenance des projets.

Dans certains cas, on peut se permettre d'avoir un "cas joker":

```ocaml
let connu_de_paul_elliot maille =
  match maille with
   | Endroit -> true
   | Envers -> true
   | _ -> false
```

Même si on rajoute un nouveau genre de point, Paul-Elliot ne le connaitra pas
pour autant.

## Le tricot, c'est plus compliqué que ça !

Bien sur, le tricot c'est plus compliqué que ça !

```ocaml
type rang = maille list
type tricot = rang list
```

## Les commits

Heureusement, on peut associer des données aux constructeurs !

```ocaml
type commit =
  | Hash of string
  | Tag of string
  | Branch of string
  | Head
  | Fetch_head
  | Orig_head
  | Merge_head;;
```

Quand on crée une valeur, on utilise la syntaxe suivante :

```ocaml
let branche_principale = Branch "main"
```
