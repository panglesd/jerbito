# Exercices sur les variants et records

On reprend tout d'abord la définition des mailles de tricot :

```ocaml
type maille =
  | Endroit
  | Envers

type maillage =
  | Maillage_endroit (** Fait une maille à l'endroit *)
  | Maillage_envers (** Fait une maille à l'endroit *)
  | Glisse (** Passe une maille d'un côté à l'autre sans la tricoter *)
  | Jete (** "Jette" une maille *)
  | Augmente (** Crée deux mailles à partir d'une seule *)
```

1. Créer la fonction `maille` qui prend en entrée une maille et un maillage, et execute le maillage !

1. Écrire la fonction `previous`, qui 
1. Ècrire `option_map` qui étant donné une valeur de type 
1. Définir un type `semaine`
2. Définir un type `carte_a_jouer`
3. Définir une fonction calculant le nombre de points d'une carte (la couleur de l'atout)
3. Définir un type 

- Ecrire la fonction `est_une_tete_noire`.
- Ecrire la fonction qui à une carte (considérée atout), associe le nombre de points à la coinche.
- Ecrire la fonction qui à une carte (considérée pas atout), associe le nombre de points à la coinche.
- Ecrire la fonction qui prend en entrée une carte, une couleur (l'atout), et associe le nombre de points à la coinche.

- Definir un type pour les points dans le plan.
- Ecrire une fonction qui 
