# Reflections — Scraping to KPI

## 1. Silent vs. loud robots.txt failure

Une erreur qui fait planter le script, on la voit tout de suite et on la corrige. Une erreur silencieuse donne un résultat faux qui a l'air normal : avec `rp.read()` derrière un proxy, le script pense que tout est interdit sans rien signaler, et dans l'autre sens on pourrait croire qu'on a le droit de scraper alors que non. Pour la provenance (CM3), c'est grave : on doit pouvoir prouver qu'on a vérifié les règles avant de récupérer une donnée, et un contrôle qui échoue sans prévenir ne prouve plus rien. Chez moi le check a bien répondu `True` pour la page Wikipédia du Mans.

## 2. France Travail data vs. jobspy sample: risk, public vs. private repo

Les données France Travail sont de l'open data avec une licence qui autorise la réutilisation, donc on a le droit de les republier. Les offres récupérées avec jobspy viennent d'Indeed/LinkedIn, dont les conditions d'utilisation interdisent de les redistribuer. Un repo public, c'est justement redistribuer à tout le monde, alors qu'un repo privé reste plutôt un usage perso, donc le risque est plus faible. Mais même en privé ce n'est pas vraiment autorisé, c'est pour ça que le `.gitignore` garde ces fichiers hors de Git dans tous les cas.

## 3. Why free-text-to-skills fits an LLM and application-tracking doesn't

Extraire des compétences d'une offre, c'est du texte libre, écrit différemment à chaque fois et parfois en français ou en anglais : une règle fixe (liste de mots-clés, regex) raterait plein de cas, alors qu'un LLM comprend le contexte. Et si le modèle se trompe un peu, on peut le vérifier en relisant l'offre. Par contre, savoir à quelles offres j'ai vraiment postulé ou quel est mon vrai niveau, c'est un fait que je connais déjà : il suffit de le noter. Un LLM ne peut que deviner, et il risque d'inventer quelque chose de faux sur une donnée qui doit être exacte.

## 4. Predicted LLM formatting inconsistency, and what I found

Ma prédiction (avant de regarder) : chaque appel au modèle est indépendant, donc la même compétence risque d'être écrite de façon différente d'une offre à l'autre, par exemple « Python » / « python », « ML » / « Machine Learning », ou « CI/CD » / « CI-CD ». Au moment de compter, ça séparerait une seule compétence en deux.

Ce que j'ai trouvé dans mon `extracted.json` (12 offres) : pas de doublon exact de majuscule, mais le même problème sous une autre forme : « CI/CD », « GitLab CI/CD » et « CI/CD pipelines » sont trois entrées différentes, pareil pour « AI » et « AI/ML ». Honnêtement, l'absence de doublon de casse vient surtout du fait que peu d'offres demandaient la même compétence (Python n'apparaît que deux fois, écrit pareil), pas d'une extraction plus fiable. J'ai aussi vu deux offres d'ingénieur avec zéro compétence extraite, ce qui est suspect.


## 5. Critique pass as human-in-the-loop

C'est du human-in-the-loop parce qu'une personne relit la sortie brute du modèle en la comparant au texte source, et peut corriger avant que les erreurs partent dans le KPI. Ça doit se faire sur `extracted.json` car c'est là qu'on voit chaque offre avec ses compétences : dans `kpi.json` tout est déjà agrégé, on ne peut plus savoir quelle offre a une compétence oubliée ou inventée. Erreur trouvée par mon binôme : [À COMPLÉTER après l'échange avec un camarade].


## 6. My own TARGET_SKILL, and which KPI value I'd trust

Mon choix : CI/CD, parce que c'est une pratique qu'on retrouve aussi bien en logiciel qu'en embarqué et qu'on en parle peu en cours. Résultat : Python = 17 % (2/12), CI/CD = 25 % (3/12). Je ne ferais confiance à aucun des deux pour dire au comité « il faut enseigner X » : 12 offres c'est trop peu (une offre de plus ou de moins change le résultat de 8 points), il y a une annonce en double dans mon échantillon, et les offres ne ressemblent pas forcément à ce que visent les étudiants de l'ENSIM.


## 7. What can be reconstructed from kpi.json alone

Dans `kpi.json` il n'y a que des pourcentages, des comptes et des noms de compétences : pas de titre d'offre, pas d'entreprise, pas de texte. C'est un choix voulu dans `compute_kpi()`, qui ne renvoie que des agrégats alors que `extracted.json` contient bien `title` et `company`. Par contre ce n'est pas parfait : avec seulement 12 offres, une compétence rare qui apparaît une seule fois (par exemple « HIL » ou « CAPL ») pourrait suffire à retrouver l'annonce d'origine en la cherchant sur internet.


## 8. Who this dashboard is really for


## 9. My second KPI, and which one I'd trust more
