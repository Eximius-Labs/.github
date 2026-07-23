<div align="center">

![Eximius Labs](https://raw.githubusercontent.com/Eximius-Labs/.github/main/profile/assets/git_banner.png)

**One model. One vector space. Text, image, video, audio.**

</div>

---

Eximius Labs builds open-weight multimodal embedding models.

Our flagship line, **Fusion Embedding**, maps text, images, video, and audio into a single
shared vector space for retrieval, RAG, clustering, and cross-modal search. The weights are
published and the models run entirely on your own hardware.

### The idea

We extend a state-of-the-art vision-language embedding base with new modalities without
modifying a single base weight. Text, image, and video vectors stay bit-for-bit identical to
the base model, so gaining a modality never costs you a re-index.

### Models

| Model | Description |
|---|---|
| [fusion-embedding-2](https://huggingface.co/EximiusLabs/fusion-embedding-2-2b-preview) | Current line. Connector plus modality-gated deep adapters, 60.6M trained parameters. |
| [fusion-embedding-1](https://huggingface.co/EximiusLabs/fusion-embedding-1-2b-preview) | Connector-only architecture, 16.4M trained parameters. Final at v0.3. |
| [Ember](https://huggingface.co/EximiusLabs/fusion-embedding-2-ember) | The first sense pack: a separately loadable adapter pack that adds thermal imagery to fusion-embedding-2 as a fifth modality, 44.2M trained parameters. |

Sense packs are named for the physical trace their sensor reads. Ember reads heat. More
senses are in training.

### Start here

- **Code:** [fusion-embedding](https://github.com/Eximius-Labs/fusion-embedding), Apache-2.0
- **Weights:** [huggingface.co/EximiusLabs](https://huggingface.co/EximiusLabs)
- **Technical report:** [arXiv:2607.18666](https://arxiv.org/abs/2607.18666)
