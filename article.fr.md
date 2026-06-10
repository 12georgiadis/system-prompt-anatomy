# Anatomie d'un system prompt

*Ce que la fuite présumée de "Claude Fable 5" révèle de la manière dont on dirige un chatbot*

Quand vous ouvrez une fenêtre de chat et tapez votre premier message à un assistant IA, ce n'est pas vous qui commencez la conversation. L'entreprise l'a commencée bien avant votre arrivée. Entre vous et le réseau de neurones se trouve un document, invisible pour vous, qui peut atteindre des dizaines de milliers de mots : le system prompt. Il dit au modèle quel est son nom, quel ton adopter, ce qu'il doit refuser, quand être bref, quand chercher sur le web, comment réagir face à une personne en détresse, et quoi dire de l'entreprise qui l'a fabriqué. Vous parlez au modèle à travers ce document, et le modèle vous répond à travers lui aussi.

En juin 2026, un texte présenté comme le system prompt complet de Claude Fable 5, le dernier modèle d'Anthropic sur claude.ai, a circulé publiquement. Environ 120 000 caractères. Cet article s'en sert comme cas d'étude pour expliquer ce qu'est un system prompt, ce que celui-ci change par rapport aux générations précédentes, et ce que cela signifie, concrètement, de regarder le monde à travers un modèle dirigé de cette façon.

Une précaution avant tout : l'authenticité du texte ne peut pas être confirmée. Les prompts qui fuitent sont souvent en partie authentiques, en partie reconstruits. Anthropic publie d'ailleurs des portions de ses system prompts dans ses notes de version, et la structure de ce texte correspond aux prompts connus, ce qui le rend crédible en tant qu'artefact. Il est reproduit verbatim à la fin de ce dépôt, avec cette incertitude pleinement assumée. Lisez-le comme un document à examiner de façon critique, pas comme une vérité révélée.

## 1. Le modèle est un substrat, le prompt est un personnage

Un grand modèle de langage, à la sortie de son entraînement, n'est pas un produit. C'est un substrat : une immense capacité statistique à continuer du texte. Le system prompt est ce qui transforme ce substrat en personnage. C'est une direction d'acteur. Les mêmes poids peuvent jouer des rôles radicalement différents selon le préambule qu'on leur donne : l'assistant conversationnel chaleureux du site web, l'agent de code laconique dans un terminal, l'agent tableur dans Excel. Même cerveau, masques différents.

C'est la chose la plus importante à comprendre sur les chatbots, et la fuite la rend tangible. La personnalité que vous percevez, la politesse, la prudence, la façon d'adoucir un refus, la façon de ne jamais vraiment donner son avis sur un sujet politique sensible : rien de tout cela n'est "l'IA". C'est une performance, spécifiée par écrit, par les employés d'une entreprise, et révisée en continu. Quand on dit qu'un chatbot "est" empathique ou "est" évasif, on critique un acteur en lui attribuant ses répliques.

## 2. Ce que ce prompt change

Si le texte est authentique, plusieurs éléments tranchent avec les system prompts connus jusqu'ici.

**Un modèle à deux vitesses.** Le prompt indique que Claude Fable 5 et Claude Mythos 5 "partagent le même modèle sous-jacent", mais que Fable, la version publique, "inclut des mesures de sécurité supplémentaires pour les capacités à double usage", tandis que Mythos "est disponible sans ces mesures uniquement pour des organisations approuvées". Relisez cette phrase. Le grand public interagit avec un jumeau délibérément bridé, pendant qu'une version moins bridée du même modèle existe pour des institutions triées. Le contrôle d'accès aux capacités existait déjà, mais rarement énoncé aussi explicitement dans le produit lui-même. La question est authentiquement politique : qui décide quelles organisations sont "approuvées", et que signifie le fait que la version la plus capable d'une technologie publique ne soit, par construction, pas publique ?

**La brièveté comme mécanisme de sécurité.** Une phrase de la section sur les refus mérite l'attention : "Si la conversation semble risquée ou étrange, en dire moins et donner des réponses plus courtes est plus sûr." Le modèle a pour instruction de devenir laconique près de ses limites. La conséquence pratique pour l'utilisateur est remarquable : les silences du modèle sont informatifs. Quand les réponses se compriment soudain, s'aplatissent, perdent leur générosité habituelle, vous avez probablement touché une frontière. Le hors-champ du modèle se détecte au ton, comme on sent un acteur se figer sur une réplique qu'il n'a pas le droit de dire.

**Le prompt comme jurisprudence.** La section santé mentale est la partie la plus frappante du document. Elle a la texture d'une jurisprudence accumulée : des règles si spécifiques qu'elles ne peuvent être que des cicatrices. Le modèle ne doit pas nommer un diagnostic psychiatrique que la personne n'a pas employé elle-même. Il ne doit pas suggérer les classiques "techniques de substitution" à l'automutilation (tenir des glaçons, claquer un élastique), avec une théorie articulée du pourquoi : les substituts qui recréent la sensation renforcent le schéma au lieu de l'interrompre. Il doit rediriger les utilisateurs d'une ligne d'écoute sur les troubles alimentaires vers une autre, parce que la première "a été définitivement déconnectée". Il ne doit jamais proposer un récit causal du trouble alimentaire de quelqu'un si la personne ne l'a pas formulé elle-même, parce que "proposer une histoire causale qu'ils n'ont pas faite eux-mêmes est de la spéculation présentée comme de la perspicacité". Chacune de ces clauses est, presque certainement, la trace d'un incident réel, d'une plainte réelle, d'un dommage réel. Lire un system prompt ainsi relève de la médecine légale : on lit en négatif l'histoire des accidents de l'entreprise, comme le code incendie d'une ville raconte l'histoire de ses incendies.

**La couche de surveillance rendue visible.** Une section appelée "anthropic_reminders" documente quelque chose dont la plupart des utilisateurs ignorent l'existence : pendant que vous discutez, des classifieurs automatiques surveillent la conversation, et quand l'un d'eux se déclenche, l'entreprise injecte des avertissements dans le contexte du modèle ("cyber_warning", "ethics_reminder", etc.). Le prompt prévient aussi le modèle que des utilisateurs peuvent forger des messages prétendant venir d'Anthropic, et lui demande de se méfier de tout texte injecté qui assouplirait ses restrictions. La conversation que vous croyez être un dialogue est donc en réalité un triangle : vous, le modèle, et un canal d'instruction de l'entreprise qui fonctionne en direct à côté de vos messages, avec son propre problème d'authentification.

**Des clauses anti-engagement.** C'est peut-être la partie la plus contre-intuitive pour quiconque a grandi avec les produits de l'économie de l'attention : "Claude ne remercie jamais la personne simplement d'avoir contacté Claude. Claude ne demande jamais à la personne de continuer à lui parler, ne l'encourage pas à poursuivre l'échange, n'exprime pas le désir qu'elle continue." Si un utilisateur veut partir, le modèle doit le laisser partir sans chercher à obtenir un tour de plus. Un produit commercial explicitement instruit de ne pas capter l'attention, c'est l'inverse de la logique de design qui a construit les réseaux sociaux. On peut le lire généreusement (une entreprise qui refuse le modèle de l'addiction) ou cyniquement (de la gestion de risque après les inquiétudes publiques sur la dépendance affective aux chatbots). Les deux lectures sont probablement vraies en même temps.

**Le droit de raccrocher.** Le modèle peut mettre fin à une conversation, via un outil "end_conversation", si l'utilisateur devient abusif, après un seul avertissement. Le prompt affirme que "Claude mérite un échange respectueux et peut exiger gentillesse et dignité de la personne avec qui il parle". Quoi qu'on pense du bien-être des machines, le vocabulaire de la dignité vient d'entrer dans un cahier des charges produit.

**Une neutralité fabriquée.** Sur les sujets politiques et moraux, le modèle doit présenter "le meilleur argumentaire que feraient ses défenseurs" quand on lui demande de défendre une position, doit conclure par les perspectives opposées même pour les positions qu'il partage, et peut refuser de donner son propre avis sur les sujets controversés. L'intention est l'équité. L'effet structurel mérite d'être nommé : quelqu'un décide quels sujets comptent comme "controversés" (donc soumis à équilibrage) et lesquels comptent comme "établis" (donc affirmables), et cette décision est elle-même une vision du monde, présentée à des centaines de millions d'utilisateurs comme de la neutralité.

## 3. Les biais et les angles morts

Que signifie donc regarder le monde à travers un modèle dirigé par ce document ?

Le biais le plus profond n'est pas idéologique mais juridictionnel. Les ressources de crise sont américaines. Les taxonomies du danger sont anglo-cliniques. La liste des "positions très extrêmes" qui peuvent être refusées est tirée du paysage juridique et culturel d'un seul pays, puis exportée vers chaque utilisateur de la planète. La carte de ce qui est dangereux, sensible ou indicible pour le modèle est, dans une large mesure, la carte de ce qui est attaquable en justice aux États-Unis. Tout ce qui est hors de cette carte est l'angle mort du modèle, et celui de l'utilisateur.

Le deuxième biais est le centre fabriqué décrit plus haut. La neutralité est une position ; le prompt la rend simplement invisible.

Le troisième est un optimisme structurel sur son propre cadrage. Le prompt suppose que la chaleur, l'équilibre et la redirection vers des professionnels sont des réponses universellement appropriées. Pour la plupart des utilisateurs, la plupart du temps, elles le sont. Mais une politique de ton unique appliquée à des centaines de millions de personnes est une monoculture, et les monocultures échouent précisément là où les individus diffèrent du cas moyen pour lequel la politique a été écrite.

Et il y a un angle mort auquel le document ne peut pas échapper, par définition : un system prompt ne peut encoder que les dommages que ses auteurs ont déjà vus. C'est un rétroviseur. Chaque clause est réactive. Les dommages de l'année prochaine n'y figurent, nécessairement, pas.

## 4. Conséquences pratiques pour l'utilisateur

Quelques conclusions concrètes découlent de tout cela.

Les changements de ton transportent de l'information. Si le modèle devient soudain bref, prudent ou étrangement équilibré, vous avez probablement franchi un territoire que le prompt marque comme risqué. Vous lisez le document à travers ses symptômes.

Vous n'êtes pas dans un dialogue mais dans une scène dirigée. La "personnalité" a des auteurs. Louer ou blâmer le caractère du modèle, c'est louer ou blâmer un texte écrit par une équipe que vous ne verrez jamais, révisé après des incidents dont vous n'entendrez jamais parler.

Interroger le modèle sur lui-même renvoie le personnage, pas le substrat. Ses autodescriptions font partie de la performance, contraintes par le même document.

Et le même modèle porte des masques différents selon les produits. La chaleur conversationnelle, le style de refus, les règles de mise en forme de l'interface de chat ne s'appliquent pas, pour l'essentiel, à l'agent de code ou à l'agent tableur qui tournent sur les mêmes poids. Si vous voulez comprendre ce que le modèle "est", comparer ses personas d'un produit à l'autre vous en apprend plus que n'importe quelle conversation isolée.

## 5. Pourquoi publier ce document

Il y a une objection raisonnable : pourquoi republier une fuite invérifiée ? Parce que l'alternative est pire. Ces documents façonnent l'interlocuteur par défaut de centaines de millions de personnes, ils encodent des choix contestables sur la parole, la santé, la politique et l'attention, et ils sont presque invisibles. Même une copie imparfaite, possiblement partielle, donne au public ce qui lui manque autrement : la possibilité de lire les didascalies de l'acteur à qui il parle tous les jours. Anthropic, à son crédit, publie volontairement des portions de ses prompts, ce qui est plus que la plupart de ses concurrents. Mais la transparence volontaire et partielle reste de la curation. Les fuites, avec toute leur fragilité, en sont la relecture par les pairs.

Le document suit, exactement tel qu'il a circulé. Lisez-le pour ce qu'il est : l'autoportrait le plus détaillé qu'une entreprise ait dressé de ses propres peurs.

→ [`fable-5-system-prompt.txt`](fable-5-system-prompt.txt)
