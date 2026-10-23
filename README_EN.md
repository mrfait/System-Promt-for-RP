## Compatibility & Setup

The framework relies on a tiered context hierarchy. How these layers are recognized depends on your client.

### Soul of Waifu
If you are using [Soul of Waifu](https://github.com/jofizcd/Soul-of-Waifu), no setup is required. All context slots, engine macros, and system injections work out of the box.

### Third-Party Frontends (SillyTavern, etc.)
When using other interfaces, ensure the model can distinguish character details, world lore, and author notes. Choose either approach:

1. **Macro Alignment:** Rename the bracketed headers inside the system prompt to match your frontend's template macros (e.g., `{{char}}`, `{{lore}}`).
2. **Manual Header Tagging:** Add the corresponding tag as a plain text header at the very top of each data field:

| Block Tag | Target Field |
|---|---|
| `[CHARACTER PROFILE]` | Character description / main card field |
| `[USER PROFILE]` | User persona description |
| `[WORLD LORE & KNOWLEDGE]` | Lorebook / World Info entries |
| `[CHARACTER PSYCHOLOGY & COGNITIVE CACHE]` | Dynamic psychological tracker / cache |
| `[AUTHOR NOTES]` | Author's Note field |
| `[RELEVANT DEEP MEMORY]` | Long-term memory / factual recall slots |
| `[Story Summary]` | Chat summary / story recap block |

---

## Character Card Preparation

Raw character cards (from Chub, W++, Boostyle, or plain text notes) often carry conflicting instructions, pseudo-RPG mechanics, or prompt leaks that compromise agency and narrative flow. 

A two-step pipeline converts raw source cards into clean, high-density payloads using any frontier LLM (ChatGPT, Claude, etc.) within a **single conversation thread**.

> Personally, I use GLM 5.3 via a subscription on NanoGPT.

### Conversion Steps:

1. **Step 1 (Initial Adaptation):**
    - Start a fresh conversation.
    - Paste your raw source card together with the contents of `CARD_ADAPTER`.
    - Wait for the compiled draft to finish.
2. **Step 2 (Verification & De-Engineering):**
    - **Do not start a new chat.** In the same conversation thread, send the contents of `CARD_VERIFIER_COMPLETER`.
    - The verifier compares the draft against the original, restores distinct dialogue quirks or subtle traits, collapses artificial pseudo-RPG trackers, and checks formatting discipline.
