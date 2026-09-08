# Chapitre 8 — Le parametre A et son ramping

`A` n'est pas fige a la creation du pool : `ramp_A`, reservee au proprietaire, permet de le faire glisser lineairement d'une valeur `initial_A` vers une `future_A` entre deux horodatages.

`_A`, appelee a chaque operation, interpole la valeur courante de `A` en fonction du temps ecoule dans la rampe. Avant `future_A_time`, elle calcule une moyenne ponderee lineaire ; apres, elle renvoie directement `future_A`.

Les gardes-fous sont stricts : la nouvelle valeur ne peut ni depasser 10 fois ni descendre sous un dixieme de la valeur actuelle (`MAX_A_CHANGE`), et le changement doit s'etaler sur au moins un jour (`MIN_RAMP_TIME`). Ces limites empechent le proprietaire de deplacer brutalement la courbe de prix et de piller les fournisseurs de liquidite par une variation soudaine.

`stop_ramp_A` fige immediatement la valeur courante, utile si une rampe en cours doit etre interrompue avant son terme prevu.

Augmenter `A` rend le pool plus efficace pres de l'equilibre mais plus vulnerable a un desequilibre extreme (perte plus rapide si un des actifs perd sa parite) ; le diminuer fait l'inverse. Le ramping progressif existe pour ajuster ce compromis sans choc pour les fournisseurs de liquidite en place.

[Chapitre suivant : frais et gouvernance](09-frais-et-gouvernance.md)
