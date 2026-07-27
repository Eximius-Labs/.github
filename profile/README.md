<div align="center">

![Eximius Labs](https://raw.githubusercontent.com/Eximius-Labs/.github/main/profile/assets/git_banner.png)

**One vector space for text, image, video, audio, and sensors — plus a perception layer. Open weights, self-hostable.**

</div>

---

Eximius Labs builds open-weight multimodal models that run entirely on your own hardware. The stack
has two complementary families.

**Fusion Embedding** is the memory layer. It maps text, images, video, audio, and sensor streams
into a single shared vector space for retrieval, RAG, clustering, and cross-modal search. The
weights are published and the models run on your own hardware.

**Fusion Perception** is the perception layer. Dense scene understanding and geometric place
recognition on a frozen vision backbone, with a projector that drops its features into the Fusion
Embedding space.

### The idea

We extend a state-of-the-art frozen base with new modalities and senses without modifying a single
base weight. Text, image, and video vectors stay bit-for-bit identical to the base model, so gaining
a modality never costs you a re-index.

### Fusion Embedding — the memory layer

| Model | Description |
|---|---|
| [fusion-embedding-2](https://huggingface.co/EximiusLabs/fusion-embedding-2-2b-preview) | Current line. Connector plus modality-gated deep adapters, 60.6M trained parameters. |
| [fusion-embedding-1](https://huggingface.co/EximiusLabs/fusion-embedding-1-2b-preview) | Connector-only architecture, 16.4M trained parameters. Final at v0.3. |
| [Ember](https://huggingface.co/EximiusLabs/fusion-embedding-2-ember) | Thermal sense pack: a separately loadable adapter pack that adds infrared to fusion-embedding-2 as a fifth modality, 44.2M trained parameters. |
| [Tremor](https://huggingface.co/EximiusLabs/fusion-embedding-2-tremor) | Inertial sense pack: reads a robot's or wearable's accelerometer as language. Ships a general base and a [Unitree-G1 head](https://huggingface.co/EximiusLabs/fusion-embedding-2-tremor-g1). |

Sense packs are named for the physical trace their sensor reads. Ember reads heat; Tremor reads
motion. More senses are in training.

### Fusion Perception — the perception layer

| Model | Description |
|---|---|
| [fusion-perception-1](https://github.com/Eximius-Labs/fusion-perception) | Frozen DINO backbone plus light heads: geometric place recognition ("where am I"), segmentation, and a projector that makes those features language-searchable in the Fusion Embedding space. |

### Start here

- **Code:** [fusion-embedding](https://github.com/Eximius-Labs/fusion-embedding) · [fusion-perception](https://github.com/Eximius-Labs/fusion-perception) — Apache-2.0
- **Weights:** [huggingface.co/EximiusLabs](https://huggingface.co/EximiusLabs)
- **Technical report:** [arXiv:2607.18666](https://arxiv.org/abs/2607.18666)
