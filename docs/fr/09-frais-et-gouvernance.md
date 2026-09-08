# Chapitre 9 — Frais et gouvernance

Chaque pool a deux taux de frais independants : `fee`, preleve sur les utilisateurs lors des echanges et des operations desequilibrees, et `admin_fee`, la part de ce premier frais qui revient au proprietaire du pool plutot qu'aux fournisseurs de liquidite.

Les changer suit un schema a delai fixe : `commit_new_fee` enregistre les nouvelles valeurs et fixe une echeance trois jours plus tard (`ADMIN_ACTIONS_DELAY`), `apply_new_fee` ne peut etre appelee qu'apres cette echeance, et `revert_new_parameters` annule le changement propose. Le transfert de propriete du pool suit exactement le meme schema en trois etapes.

Ce delai de trois jours est la seule protection des fournisseurs de liquidite contre un changement brutal des conditions du pool : il leur laisse le temps de retirer leurs fonds avant qu'une hausse de frais ne s'applique.

`withdraw_admin_fees` transfere au proprietaire l'ecart entre le solde ERC-20 reel du contrat et `balances` : c'est exactement les frais admin accumules, jamais les fonds des fournisseurs de liquidite. `kill_me` et `unkill_me` donnent au proprietaire un interrupteur d'urgence qui bloque les depots et les echanges desequilibres pendant au plus deux mois, sans jamais empecher un retrait proportionnel classique.

[Chapitre suivant : pools de pret et pools eth](10-pools-de-pret.md)
