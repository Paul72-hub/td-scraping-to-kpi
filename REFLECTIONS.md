# Reflections — Scraping to KPI

## 1. Silent vs. loud robots.txt failure

Une erreur qui fait planter le script, on la voit tout de suite et on la corrige. Une erreur silencieuse donne un résultat faux qui a l'air normal : avec `rp.read()` derrière un proxy, le script pense que tout est interdit sans rien signaler, et dans l'autre sens on pourrait croire qu'on a le droit de scraper alors que non. Pour la provenance (CM3), c'est grave : on doit pouvoir prouver qu'on a vérifié les règles avant de récupérer une donnée, et un contrôle qui échoue sans prévenir ne prouve plus rien. Chez moi le check a bien répondu `True` pour la page Wikipédia du Mans.

## 2. France Travail data vs. jobspy sample: risk, public vs. private repo

Les données France Travail sont de l'open data avec une licence qui autorise la réutilisation, donc on a le droit de les republier. Les offres récupérées avec jobspy viennent d'Indeed/LinkedIn, dont les conditions d'utilisation interdisent de les redistribuer. Un repo public, c'est justement redistribuer à tout le monde, alors qu'un repo privé reste plutôt un usage perso, donc le risque est plus faible. Mais même en privé ce n'est pas vraiment autorisé, c'est pour ça que le `.gitignore` garde ces fichiers hors de Git dans tous les cas.

## 3. Why free-text-to-skills fits an LLM and application-tracking doesn't

Extraire des compétences d'une offre, c'est du texte libre, écrit différemment à chaque fois et parfois en français ou en anglais : une règle fixe (liste de mots-clés, regex) raterait plein de cas, alors qu'un LLM comprend le contexte. Et si le modèle se trompe un peu, on peut le vérifier en relisant l'offre. Par contre, savoir à quelles offres j'ai vraiment postulé ou quel est mon vrai niveau, c'est un fait que je connais déjà : il suffit de le noter. Un LLM ne peut que deviner, et il risque d'inventer quelque chose de faux sur une donnée qui doit être exacte.

## 4. Predicted LLM formatting inconsistency, and what I found


## 5. Critique pass as human-in-the-loop


## 6. My own TARGET_SKILL, and which KPI value I'd trust


## 7. What can be reconstructed from kpi.json alone


## 8. Who this dashboard is really for


## 9. My second KPI, and which one I'd trust more
