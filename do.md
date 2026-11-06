Utilise l'agent `django-hexagonal-quality-auditor` en mode STRICT READ-ONLY.

Réalise une revue complète et indépendante de la fonctionnalité refactorisée, conformément à `docs/ai-review/AUDIT_SCOPE.md` et au skill associé.

Je veux deux parties distinctes :

**1. Ce qui est bien implémenté :** qualité du code, respect de l'architecture hexagonale, bonnes pratiques Python/Django, gestion correcte des exceptions, tests pertinents et décisions techniques justifiées.

**2. Ce qui doit être corrigé ou amélioré :** bugs, risques de régression, violations architecturales, code inutile ou complexe, mauvaises pratiques, erreurs Redis/Celery, défauts de validation, tests manquants, problèmes de couverture, formatage et maintenabilité.

Pour chaque anomalie, fournis sa gravité, son emplacement précis, les preuves, les risques, la correction recommandée et les tests nécessaires.

Distingue les défauts confirmés des améliorations facultatives. Produis un plan de correction priorisé pour un autre agent.

**Ne modifie absolument aucun fichier. N'exécute aucune commande. Ne corrige rien. Présente uniquement le rapport dans la conversation.**
