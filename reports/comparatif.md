# Comparatif des approches - projet fraude (TP04)

Mesures realisees le 22/10/2026 sur un PC portable (Windows, Python 3.13.6, FLAML 2.7.0).
Informations cloud relevees dans les documentations officielles le 22/10/2026.

| Approche | F1 test | Temps humain | Temps machine | Cout estime (source, date) | Explicabilite | Export / reversibilite |
|---|---|---|---|---|---|---|
| Logistique (ref.) | 0.7407 | ~5 min | 0.1 s | 0 (poste local) | Maximale | Total |
| Manuel (TP2) | 0.8669 | ~2 h (essais du TP2) | 1.09 s | 0 (poste local) | Moyenne/Bonne | Total |
| FLAML 60 s | 0.8582 | ~10 min | 60.6 s (199 essais) | 0 (poste local) | Moyenne/Basse (journal des essais) | Total |
| Vertex AI AutoML | non mesure | ~1 h (projet, facturation, import) | non mesure | 21.252 USD / noeud-heure d'entrainement + deploiement facture a l'heure (Google Cloud pricing, 22/10/2026) | Bonne (attributions des variables) | Moyenne : export vers Cloud Storage puis Docker |
| SageMaker Autopilot | non mesure | ~1 h (compte, domaine, Canvas) | non mesure | Instances de calcul a l'heure, ex. ml.c5.xlarge 0.204 USD/h (AWS SageMaker pricing, 22/10/2026) | Bonne (rapports + notebooks generes) | Faible : endpoint heberge, pas d'export documente |
| Azure Automated ML | non mesure | ~1 h (abonnement, espace de travail) | non mesure | Pas de frais de service, calcul facture a l'heure (Azure ML pricing, 22/10/2026) | Bonne (importance des variables, Responsible AI) | Bonne : fichier .pkl, conversion ONNX |

## Commentaire

1. La regression logistique sert de plancher : rapide et lisible, mais trop faible pour la fraude (F1 0.74).
2. Le reglage manuel reste le meilleur ici (0.8669) car il reutilise ce qu'on a appris au TP2 : on le garde quand on connait deja bien le probleme.
3. FLAML s'en approche en 60 s sans connaissance prealable (0.8582) : c'est l'outil ideal pour obtenir vite une base solide sur un nouveau probleme.
4. Les plateformes managees se justifient pour une equipe deja sur ce cloud, avec de gros volumes et un besoin de deploiement, de monitoring et de gouvernance integres.
5. Leur cout et la dependance au fournisseur (export limite) les rendent peu adaptees a un petit projet comme celui-ci, ou une bibliotheque locale suffit.
