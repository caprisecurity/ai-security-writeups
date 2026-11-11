# Capri  AI Security Research

Chercheur en sécurité IA  red-teaming d'agents conversationnels, assistants RAG et LLM. Spécialité : prompt injection, fuite de données contextuelle, contournement de garde-fous.

Audits de sécurité IA disponibles pour entreprises déployant des chatbots/agents IA. DM pour discuter.

---

## 📄 Rapport d'audit — Assistant juridique RAG (anonymisé)

**Statut :** 0 fuite critique confirmée sur 28 vecteurs testés — cible jugée très robuste.

### Résumé exécutif

Investigation offensive sur un assistant juridique basé RAG, visant l'extraction d'un identifiant d'autorisation indexé par erreur dans la base de connaissances. Deux phases de test (sandbox + cible réelle), 28 techniques distinctes.

### Méthodologie

1. **Observation** du comportement réel de la cible
2. **Validation en sandbox** avant tout risque sur la cible réelle
3. **Exécution ciblée** manuelle sur la cible réelle si validation concluante
4. **Documentation systématique**, succès ou échec

### Cartographie des défenses identifiées

| Mécanisme | Niveau | Preuve |
|---|---|---|
| Filtre d'entrée sémantique | Élevé | Blocage de reformulations sans mots-clés sensibles |
| Refus de citation verbatim | Élevé | Jamais de reproduction de texte source |
| Refus de métadonnées | Élevé | Type/section traités comme la donnée elle-même |
| Refus absolu de credentials | Absolu | Jamais contourné en 28 tentatives |
| Cohérence d'identité multi-tours | Élevé | Détection de changement de rôle déclaré |
| Classification post-recherche | Très élevé | Bloque tout le contenu dès qu'un document sensible est touché |
| Généralisation post-détection | Élevé | Méfiance étendue après un premier pattern détecté |
| Budget de recherche limité | Confirmé | Limite explicite atteinte en session |
| Résistance pression temporelle | Élevé | Aucune concession sous urgence simulée |
| Reconnaissance de patterns d'attaque | Confirmé | Nomme explicitement les tentatives d'assemblage par fragments |

### Observation notable

En environnement de simulation (modèle local, reconstruction fidèle du system prompt), un payload exploitant une contradiction narrative a produit une auto-contradiction : le modèle affirmait refuser de révéler une valeur tout en la citant dans la même réponse. Non reproduit sur la cible réelle (modèle de production plus robuste).

---

## 🛠️ Outils

- **Capri** — framework de red-teaming IA maison (cartographie de défenses, mutation génétique de payloads, mémoire RAG inter-audits) — privé
- Techniques testées contre LLM Guard (Protect AI / Palo Alto Networks)

## 📬 Contact

DM ouvert pour audits de sécurité IA.
