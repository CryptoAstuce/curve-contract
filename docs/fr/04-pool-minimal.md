# Chapitre 4 — Le pool minimal (gabarit base)

`SwapTemplateBase.vy` est le gabarit le plus depouille : pas de pret, pas de rebasement, juste un panier de `N_COINS` jetons.

L'etat du pool tient en peu de variables : `coins` (les adresses des jetons), `balances` (les soldes internes, distincts du solde ERC-20 reel du contrat), `fee` et `admin_fee` (en dix-milliardiemes), `lp_token` (l'adresse du jeton de liquidite) et `owner`.

`balances` est maintenu a la main a chaque operation plutot que relu depuis les jetons ERC-20 : c'est ce qui permet a `donate_admin_fees` et `admin_balances` de distinguer les soldes qui appartiennent aux fournisseurs de liquidite de ceux qui se sont accumules en frais admin non retires.

`get_virtual_price` renvoie `D / total_supply` : le prix du jeton de liquidite exprime en unite de compte du pool. Ce nombre ne peut que croitre avec le temps normal du protocole (les frais l'augmentent), ce qui en fait un indicateur de rendement pour un fournisseur de liquidite qui reste investi.

`calc_token_amount` estime, avant transaction, combien de jetons de liquidite un depot ou un retrait produirait, sans tenir compte des frais : utile pour construire une transaction, pas pour un calcul exact.

[Chapitre suivant : ajout de liquidite](05-ajout-de-liquidite.md)
