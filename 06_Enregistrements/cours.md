# Enregistrements

Les cartes à jouer sont en nombre fini, énumérons les dans un type OCaml :

```ocaml
type carte =
  | As_de_coeur
  | Sept_de_coeur
  | Huit_de_coeur
  | Neuf_de_coeur
  | Dix_de_coeur
  | Valet_de_coeur
  | Dame_de_coeur
  | Roi_de_coeur
  | As_de_trefle
  | Sept_de_trefle
  | Huit_de_trefle
  | Neuf_de_trefle
  | Dix_de_trefle
  | Valet_de_trefle
  | Dame_de_trefle
  | Roi_de_trefle
  | As_de_pique
  | Sept_de_pique
  | Huit_de_pique
  | Neuf_de_pique
  | Dix_de_pique
  | Valet_de_pique
  | Dame_de_pique
  | Roi_de_pique
  | As_de_carreau
  | Sept_de_carreau
  | Huit_de_carreau
  | Neuf_de_carreau
  | Dix_de_carreau
  | Valet_de_carreau
  | Dame_de_carreau
  | Roi_de_carreau
```

Heureusement que ce n'est pas un jeu de tarot !

Maintenant, écrivons la fonction qui donne la couleur étant donné la carte... Pas très utilisable !

Faisons un autre essais :

```ocaml
type couleur = Pique | Coeur | Carreau | Trefle

type carte =
  | As of couleur
  | Sept of couleur
  | Huit of couleur
  | Neuf of couleur
  | Dix of couleur
  | Valet of couleur
  | Dame of couleur
  | Roi of couleur
```

Toujours pas super


## Un jeu de coinche en OCaml

```ocaml
type couleur = Pique | Coeur | Carreau | Trefle

type force = As | Sept | Huit | Neuf| Dix | Valet | Dame | Roi

type carte = {couleur : couleur ; force : force}
```

Mais qu'est-ce que cela peut bien vouloir dire ?

Un type enregistrement a des champs, qui peuvent prendre toutes les valeurs du
type associé au champs, indépendament les uns des autres (par exemple si on a
perdu le 7 de pique, impossible d'enlever cette valeur spécifique du type au
dessus !).

Quelques exemples de syntaxe :

```ocaml
let reine_de_coeur = { couleur = Coeur ; force = Reine}

(** Comme les champs sont nommés, l'ordre n'a pas d'importance: *)
let reine_de_coeur = { force = Reine; couleur = Coeur }

(** On peut accéder à un champs avec un point *)
let force_de carte = carte.force
let couleur_de carte = carte.couleur

(** On peut filtrer sur les cartes! *)
let force_et_couleur carte =
  match carte with
   | { force ; couleur } -> {couleur ; force}

(** Cela prend tout son sens quand on filtre les champs ! *)
let est_un_valet_rouge carte =
  match carte with
   | { force = Valet ; couleur = Coeur } -> true
   | { force = Valet ; couleur = Carreaux } -> true
   | _ -> false

let est_un_valet_rouge carte =
  match carte with
   | { force = Valet ; couleur = (Coeur | Carreaux) } -> true
   | _ -> false
```

## Tuples : enregistrements ordonés plutôt que nommés

```ocaml
type carte = couleur * force
```

## Un type enregistrement plus sérieux

```ocaml
type ethique = Loyal | E_Neutre | Chaotique

type moral = Bon | M_Neutre | Mauvais

type personnage = {
  nom : string;
  niveau : int;
  race : string;
  alignement : firmness * rectitude;
  classe_d_armure : int;
};;
```

```ocaml
let ghorghor_bey = {
    nom = "Ghôrghôr Bey";
    niveau = 17;
    race = "half-ogre";
    alignement = (Chaotique, M_Neutre);
    armor_class = -8;
  };;
```

```ocaml
ghorghor_bey.alignment;;
```
```ocaml
ghorghor_bey.level;;
```
