# Chapitre 5 — Ajout de liquidite

`add_liquidity` accepte un depot dans n'importe quelle proportion entre les `N_COINS` jetons du pool, contrairement a un AMM a deux jetons qui exige un ratio fixe.

Le calcul se fait en trois temps. `D0` est l'invariant avant depot. Les soldes sont augmentes des montants deposes, ce qui donne `D1`, toujours superieur a `D0`. Puis, si le pool n'est pas vide, une commission proportionnelle a l'ecart entre le nouveau solde et le solde « ideal » (celui qui aurait garde les proportions identiques) est prelevee sur chaque jeton : c'est le mecanisme qui decourage les depots desequilibres, puisqu'ils coutent plus cher en frais.

Apres deduction des frais, l'invariant final `D2` sert a calculer le nombre de jetons de liquidite a emettre : `mint_amount = total_supply * (D2 - D0) / D0`. Le tout premier depot echappe aux frais et recoit directement `D1` jetons.

Chaque jeton deplace passe par `transferFrom`, avec une gestion manuelle du retour de la fonction pour accepter aussi bien les jetons conformes a la norme que les jetons comme USDT qui ne renvoient rien.

[Chapitre suivant : l'echange entre jetons](06-echange.md)
