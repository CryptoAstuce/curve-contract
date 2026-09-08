# Chapitre 3 — L'invariant StableSwap

Le coeur mathematique de Curve est la fonction `_get_D`, dans `SwapTemplateBase.vy`. Elle resout par iteration l'equation qui definit `D`, l'invariant du pool : `A * n**n * sum(x_i) + D = A * D * n**n + D**(n+1) / (n**n * prod(x_i))`.

`A` est le facteur d'amplification. Quand `A` est petit, l'equation se rapproche du produit constant `prod(x_i) = k` de type Uniswap. Quand `A` est grand, elle se rapproche de la somme constante `sum(x_i) = k`, qui echange a taux quasi fixe. Curve choisit un `A` eleve pour des actifs qui doivent normalement valoir la meme chose, ce qui rend le prix quasi plat pres de l'equilibre tout en gardant une courbe de produit constant comme filet de securite si le pool se desequilibre fortement.

La resolution se fait par la methode de Newton : `_get_D` part de `D = somme des soldes` et affine la valeur sur au plus 255 iterations, jusqu'a ce que deux valeurs successives different d'au plus 1. La convergence reelle prend generalement quatre iterations.

`_xp` convertit les soldes bruts en valeurs de precision uniforme 1e18 via le tableau `RATES`, avant tout calcul : c'est ce qui permet a un pool de melanger des jetons a 6 et 18 decimales sans fausser l'invariant.

[Chapitre suivant : le pool minimal](04-pool-minimal.md)
