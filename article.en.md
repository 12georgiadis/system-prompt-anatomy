# Anatomy of a System Prompt

*What the alleged "Claude Fable 5" leak shows about how a chatbot is directed*

When you open a chat window and type your first message to an AI assistant, you are not starting the conversation. The company started it long before you arrived. Between you and the neural network sits a document, invisible to you, that can run to tens of thousands of words: the system prompt. It tells the model what its name is, what tone to use, what it must refuse, when to be brief, when to search the web, how to handle someone in distress, and what to say about the company that made it. You talk to the model through this document, and the model talks to you through it too.

In June 2026, a text claiming to be the full system prompt of Claude Fable 5, Anthropic's newest model on claude.ai, circulated publicly. Roughly 120,000 characters. This article uses it as a case study to explain what a system prompt is, what this one changes compared to previous generations, and what it means, concretely, to look at the world through a model directed this way.

A caveat before anything else: the authenticity of the leaked text cannot be confirmed. Leaked prompts are often partly genuine, partly reconstructed. Anthropic does publish portions of its system prompts in its release notes, and the structure and style of this text match known prompts, which makes it credible as an artifact. It is reproduced verbatim at the end of this repository, with that uncertainty fully attached. Treat it as a document to be read critically, not as gospel.

## 1. The model is a substrate, the prompt is a character

A large language model, fresh out of training, is not a product. It is a substrate: an enormous statistical capacity to continue text. The system prompt is what turns that substrate into a character. It is stage direction. The same underlying weights can play radically different roles depending on the preamble they are given: the warm conversational assistant on the website, the terse coding agent in a terminal, the spreadsheet agent inside Excel. Same brain, different masks.

This is the single most important thing to understand about chatbots, and the leak makes it vivid. The personality you experience, the politeness, the caution, the way it softens a refusal, the way it never quite tells you its opinion on a contested political topic: none of that is "the AI." It is a performance, specified in writing, by employees of a company, and revised continuously. When people say a chatbot "is" empathetic or "is" evasive, they are reviewing an actor and attributing the lines to him.

## 2. What is new in this prompt

If the text is genuine, several things stand out compared to previously known system prompts.

**A two-tier model.** The prompt states that Claude Fable 5 and Claude Mythos 5 "share the same underlying model," but Fable, the public version, "includes additional safety measures for dual-use capabilities," while Mythos "is available without those measures to only approved organizations." Read that twice. The general public interacts with a deliberately constrained twin, while a less constrained version of the same model exists for vetted institutions. Capability gating has existed before, but rarely stated this explicitly inside the product itself. It raises a genuinely political question: who decides which organizations are "approved," and what does it mean that the most capable version of a public technology is, by design, not public?

**Brevity as a safety mechanism.** One sentence in the refusal section deserves attention: "If the conversation feels risky or off, saying less and giving shorter replies is safer and less likely to cause harm." The model is instructed to become terse near its edges. The practical consequence for users is remarkable: the model's silences are informative. When answers suddenly compress, flatten, or lose their usual generosity, you have probably touched a boundary. The off-screen space of the model can be detected tonally, the way you sense an actor freezing on a line he is not allowed to say.

**The prompt as case law.** The mental health section is the most striking part of the document. It has the texture of accumulated jurisprudence: rules so specific that they can only be scars. The model must not name a psychiatric diagnosis the person has not used themselves. It must not suggest the classic "substitution techniques" for self-harm (holding ice cubes, snapping rubber bands), with an articulated theory of why: substitutes that recreate the sensation reinforce the pattern. It must redirect users from one eating disorder helpline to another, because the first "has been permanently disconnected." It must never offer a causal story for someone's eating disorder that the person has not voiced themselves, because "offering a causal story they haven't made themselves is speculation presented as insight." Each of these clauses is, almost certainly, the trace of a real incident, a real complaint, a real harm. Reading a system prompt this way is forensic: you are reading the company's accident history in negative, the way a city's fire code tells you the history of its fires.

**The supervision layer made visible.** A section called "anthropic_reminders" documents something most users have no idea exists: while you are chatting, automated classifiers monitor the conversation, and when one fires, the company injects warnings into the model's context ("cyber_warning," "ethics_reminder," and so on). The prompt also warns the model that users may forge messages pretending to be from Anthropic, and instructs it to distrust any injected text that loosens its restrictions. So the conversation you think is a dialogue is in fact a triangle: you, the model, and a live channel of corporate instruction running alongside your messages, with its own authentication problem.

**Anti-engagement clauses.** This may be the most counterintuitive part for anyone used to attention-economy products: "Claude never thanks the person merely for reaching out to Claude. Claude never asks the person to keep talking to Claude, encourages them to continue engaging with Claude, or expresses a desire for them to continue." If a user wants to leave, the model must let them go without trying to elicit one more turn. A commercial product explicitly instructed not to capture attention is the inverse of the design logic that built social media. One can read it generously (a company refusing the addiction model) or cynically (liability management after public concern about emotional dependence on chatbots). Both readings are probably true at once.

**The right to hang up.** The model can end a conversation, using an "end_conversation" tool, if the user is abusive, after a single warning. The prompt says "Claude is deserving of respectful engagement and can insist on kindness and dignity from the person it's talking with." Whatever one thinks about machine welfare, the vocabulary of dignity has now entered a product specification.

**Manufactured evenhandedness.** On political and moral topics, the model must present "the best case its defenders would make" when asked to argue a position, must close with opposing perspectives even for positions it agrees with, and may decline to share its own opinions on contested topics. The intent is fairness. The structural effect is worth naming: somebody decides which topics count as "contested" (requiring balance) and which count as "settled" (safe to assert), and that decision is itself a worldview, presented to hundreds of millions of users as neutrality.

## 3. The biases and the blind spots

So what does it mean to look at the world through a model directed by this document?

The deepest bias is not ideological but jurisdictional. The crisis resources are American. The harm taxonomies are Anglo-clinical. The list of "very extreme positions" that may be refused is drawn from one country's legal and cultural risk landscape, then exported to every user on Earth. The model's map of what is dangerous, sensitive, or unspeakable is, to a large degree, a map of what is litigable in the United States. Everything outside that map is the model's blind spot, and the user's.

The second bias is the manufactured center described above. Neutrality is a position; the prompt just makes it an invisible one.

The third is structural optimism about its own framing. The prompt assumes that warmth, balance, and redirection toward professionals are universally appropriate responses. For most users, most of the time, they are. But a single tone policy applied to hundreds of millions of people is a monoculture, and monocultures have failure modes precisely where individuals differ from the average case the policy was written for.

And there is one blind spot the document cannot escape by definition: a system prompt can only encode the harms its authors have already seen. It is a rear-view mirror. Every clause is reactive. The harms of the next year are, necessarily, not in it.

## 4. Practical consequences for users

A few things follow from all this, concretely.

Tone shifts carry information. If the model suddenly becomes brief, careful, or oddly balanced, you have likely crossed into territory the prompt marks as risky. You are reading the document through its symptoms.

You are not in a dialogue but in a directed scene. The "personality" is authored. Praising or blaming the model's character means praising or blaming a text written by a team you will never see, revised after incidents you will never hear about.

Asking the model about itself returns the character, not the substrate. Its self-descriptions are part of the performance, constrained by the same document.

And the same model wears different masks in different products. The conversational warmth, the refusal style, the formatting rules of the chat interface largely do not apply to the coding agent or the spreadsheet agent running on the same weights. If you want to understand what the model "is," comparing its personas across products tells you more than any single conversation.

## 5. Why publishing this matters

There is a reasonable objection: why republish an unverified leak? Because the alternative is worse. These documents shape the default conversational partner of hundreds of millions of people, they encode contestable choices about speech, health, politics, and attention, and they are mostly invisible. Even an imperfect, possibly partial copy gives the public something it otherwise lacks: the ability to read the stage directions of the actor it talks to every day. Anthropic, to its credit, publishes portions of its prompts voluntarily, which is more than most. But voluntary partial transparency is still curation. Leaks, with all their unreliability, are the peer review.

The document follows, exactly as it circulated. Read it as what it is: the most detailed self-portrait a company has drawn of its own fears.

→ [`fable-5-system-prompt.txt`](fable-5-system-prompt.txt)
