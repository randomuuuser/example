**Interfaces**
- `Multimodal` — contrat pour toute tâche qui consomme ou produit plusieurs types de médias (texte, audio, image). *Ex : un modèle qui prend une image ET du texte en entrée.*
- `Agentic` — contrat pour toute tâche qui utilise des outils externes et itère en boucle. *Ex : un agent qui appelle une API météo pour répondre.*

---

**Racine & branches**
- `NLPTask` — classe mère de tout ; porte les attributs communs à toutes les tâches NLP. *Ex : `model_name`, `language`.*
- `NLPDiscriminativeTask` — regroupe les tâches qui *analysent* un texte existant pour en extraire une information (label, span, score). *Ex : détecter le sentiment d'un avis client.*
- `NLPGenerativeTask` — regroupe les tâches qui *produisent* du texte nouveau à partir d'une entrée. *Ex : générer un résumé, une réponse, du code.*
- `NLPRepresentationTask` — regroupe les tâches qui *transforment* du texte en représentation numérique exploitable (vecteur, score, cluster). *Ex : encoder des phrases pour une recherche sémantique.*
- `AudioTask` — branche dédiée aux tâches dont l'entrée ou la sortie est un signal audio. *Ex : transcrire un appel téléphonique.*
- `VisionLanguageTask` — branche dédiée aux tâches qui combinent image et langage. *Ex : décrire le contenu d'un document scanné.*

---

**Discriminatif — classification de séquence**
- `SequenceClassificationTask` — assigne un label à une séquence de texte entière. *Ex : classifier un email comme spam ou non.*
- `SentimentAnalysisTask` — cas particulier : le label est une polarité (positif/négatif/neutre), éventuellement par aspect. *Ex : analyser les avis produits sur un e-commerce.*
- `IntentDetectionTask` — cas particulier : le label est l'intention de l'utilisateur dans une phrase. *Ex : chatbot qui détecte "réserver un vol" dans "je veux partir à Paris".*
- `NLITask` — détermine si une hypothèse est entailed/contradicted/neutral par rapport à une prémisse. *Ex : vérification automatique de faits.*
- `DocumentClassificationTask` — comme `SequenceClassification` mais sur des textes longs avec chunking. *Ex : classer des contrats juridiques par type.*
- `LanguageDetectionTask` — identifie la langue d'un texte. *Ex : router automatiquement un ticket support vers le bon agent.*

---

**Discriminatif — classification de tokens**
- `TokenClassificationTask` — assigne un label à chaque token individuellement. *Ex : annoter chaque mot d'une phrase avec son rôle.*
- `NERTask` — cas particulier : les labels sont des entités nommées (personne, lieu, organisation). *Ex : extraire les noms de sociétés dans des articles financiers.*
- `POSTaggingTask` — cas particulier : les labels sont des catégories grammaticales. *Ex : pipeline de parsing syntaxique.*

---

**Discriminatif — QA & extraction**
- `QATask` — tâche de question-réponse, abstraite sur le mode de production de la réponse. *Ex : répondre à "quel est le délai de livraison ?" sur un contrat.*
- `ExtractiveQATask` — la réponse est un span extrait textuellement du contexte, sans génération. *Ex : SQuAD-style, surligner la réponse dans un paragraphe.*
- `FillMaskTask` — prédit le token masqué dans une phrase (paradigme MLM/BERT). *Ex : "La capitale de la France est [MASK]."*

---

**Génératif — completion**
- `CompletionTask` — génération libre de texte à partir d'un prompt, paradigme LLM autorégressif. *Ex : répondre à une question ouverte avec GPT-style.*
- `CodeGenerationTask` — spécialisation de completion pour produire du code dans un langage cible. *Ex : générer une fonction Python à partir d'une docstring.*
- `DialogueTask` — completion en mode conversationnel avec historique de messages. *Ex : assistant support client multi-tours.*

---

**Génératif — seq2seq**
- `Seq2SeqTask` — génération conditionnée sur un texte source entier, paradigme encoder-decoder. *Ex : T5, BART.*
- `MachineTranslationTask` — traduit un texte d'une langue source vers une langue cible. *Ex : traduire des sous-titres FR→EN.*
- `SummarizationTask` — condense un texte long en un résumé plus court. *Ex : résumer des rapports financiers.*
- `TextStyleTransferTask` — réécrit un texte en changeant son style sans changer son sens. *Ex : rendre un texte formel → informel.*

---

**Génératif — agentique**
- `RagTask` — combine une recherche dans une base de connaissance (via `EmbeddingTask`) et une génération (via `CompletionTask`) pour répondre de façon fondée. *Ex : chatbot qui répond sur la base de la doc interne.*
- `AgentTask` — planifie et exécute des actions en boucle en appelant des outils jusqu'à atteindre un objectif. *Ex : agent qui recherche, compare et synthétise des informations de plusieurs sources.*

---

**Représentation**
- `EmbeddingTask` — encode du texte (ou autre modalité) en vecteur dense dans un espace sémantique. *Ex : encoder des phrases pour alimenter un moteur de recherche vectoriel.*
- `SentenceSimilarityTask` — calcule un score de similarité entre deux textes. *Ex : détecter des doublons dans une FAQ.*
- `RankingTask` — ordonne une liste de candidats par pertinence par rapport à une requête. *Ex : reranking de résultats de recherche.*
- `TopicModelingTask` — découvre les thèmes latents d'un corpus sans supervision. *Ex : identifier les sujets récurrents dans des tickets support.*
- `ClusteringNLPTask` — regroupe des textes similaires en clusters sans labels prédéfinis. *Ex : segmenter automatiquement une base de verbatims clients.*

---

**Audio**
- `AudioTask` — base commune à toutes les tâches audio, porte les attributs du signal. *Ex : `sample_rate`, `audio_format`.*
- `ASRTask` — transcrit de l'audio en texte (Automatic Speech Recognition). *Ex : transcrire des réunions Teams.*
- `TTSTask` — synthétise de l'audio à partir de texte (Text-to-Speech). *Ex : générer une voix pour un assistant vocal.*
- `AudioToAudioTask` — transforme un signal audio en un autre signal audio. *Ex : conversion de voix, séparation de sources.*
- `AudioProcessingTask` — traitement du signal audio sans transcription ni synthèse. *Ex : nettoyage, segmentation.*
- `SpeakerDiarizationTask` — identifie et segmente les tours de parole par locuteur. *Ex : "qui parle quand" dans un podcast.*
- `AudioEnhancementTask` — améliore la qualité audio en réduisant le bruit ou les artefacts. *Ex : débruitage d'un enregistrement terrain.*

---

**Vision × Language**
- `VisionLanguageTask` — base commune aux tâches qui combinent une image et du langage. *Ex : attributs communs à OCR, captioning, VQA.*
- `OCRTask` — extrait le texte contenu dans une image ou un document scanné. *Ex : numériser des factures papier.*
- `ImageCaptioningTask` — génère une description textuelle d'une image. *Ex : accessibilité automatique d'images sur un site web.*
- `VisualQATask` — répond à une question en langage naturel en s'appuyant sur une image. *Ex : "combien de personnes sont sur cette photo ?"*