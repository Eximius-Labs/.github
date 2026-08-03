<div align="center">

![Eximius Labs](https://raw.githubusercontent.com/Eximius-Labs/.github/main/profile/assets/git_banner.png)

**Open models that give machines senses. Touch, heat, motion and sound, in one
language-searchable space, with the memory and control layers around it.
Open weights, self-hostable.**

</div>

---

A robot's cameras are well served. Its other senses are not. A pressure array, a thermal
frame, an inertial trace and an audio clip all arrive as numbers that no model reads and
nobody can search.

Eximius Labs builds the models that read them. We freeze a strong multimodal base and
attach senses from the outside, so adding a sensor costs a small trained head instead of a
new foundation model, and every embedding you have already stored stays valid. Everything
runs on your own hardware.

Measured on held-out data: an open model that recognizes objects from a $10 pressure glove
above the accuracy of the dataset authors' own supervised CNN; thermal-to-text retrieval
lifted from 0.224 to 0.785; a hospital bed mat answering plain-English posture queries at
0.957.

The stack has four layers: sense, perceive, remember, act.

**Fusion Embedding** is the embedding layer. It maps text, images, video, audio, and sensor streams
into a single shared vector space for retrieval, RAG, clustering, and cross-modal search. The
weights are published and the models run on your own hardware.

**Fusion Perception** is the perception layer. Dense scene understanding and geometric place
recognition on a frozen vision backbone, with a projector that drops its features into the Fusion
Embedding space.

**Engram** is the memory layer. It indexes a robot's video, audio, motion, and touch into that shared space
on one clock and answers questions about it in plain language, including temporal reasoning that
retrieval alone cannot do. Try it in the [live playground](https://www.eximiuslabs.com/playground).

**Efferent** is the control layer. It carries a trained policy out to a robot: any ONNX control
policy, any robot, bound by joint name rather than by hand-maintained index arrays, with a
pre-flight doctor that catches the joint-order, frame, and scale bugs that make robots fall.

### The idea

We extend a state-of-the-art frozen base with new modalities and senses without modifying a single
base weight. Text, image, and video vectors stay bit-for-bit identical to the base model, so gaining
a modality never costs you a re-index.

### Fusion Embedding — the embedding layer

| Model | Description |
|---|---|
| [fusion-embedding-2](https://huggingface.co/EximiusLabs/fusion-embedding-2-2b-preview) | Current line. Connector plus modality-gated deep adapters, 60.6M trained parameters. |
| [fusion-embedding-1](https://huggingface.co/EximiusLabs/fusion-embedding-1-2b-preview) | Connector-only architecture, 16.4M trained parameters. Final at v0.3. |
| [Ember](https://huggingface.co/EximiusLabs/fusion-embedding-2-ember) | Thermal sense pack: a separately loadable adapter pack that adds infrared to fusion-embedding-2 as a fifth modality, 44.2M trained parameters. |
| [Tremor](https://huggingface.co/EximiusLabs/fusion-embedding-2-tremor) | Inertial sense pack: reads a robot's or wearable's accelerometer as language. Ships a general base and a [Unitree-G1 head](https://huggingface.co/EximiusLabs/fusion-embedding-2-tremor-g1). |
| [Tactus](https://huggingface.co/EximiusLabs/fusion-embedding-2-tactus) | Tactile sense pack: embeds 32x32 pressure/taxel arrays (FSR gloves, e-skins, robot hands) into the shared space; matches, and at best exceeds, the STAG (Nature 2019) supervised baseline while remaining open-vocabulary. |
| [Tactus Mat](https://huggingface.co/EximiusLabs/fusion-embedding-2-tactus-mat) | The same tactile pack trained for a 64x32 body pressure mat (bed, seat, wheelchair, insole): 17 in-bed postures as open-vocabulary text queries, 0.957 top-1 on held-out subjects. |

Sense packs are named for the physical trace their sensor reads. Ember reads heat; Tremor reads
motion; Tactus reads touch. A pack can ship several sensor profiles: Tactus reads a pressure
glove, Tactus Mat the same signal class at body scale. More senses are in training.

### Fusion Perception — the perception layer

| Model | Description |
|---|---|
| [fusion-perception-1](https://github.com/Eximius-Labs/fusion-perception) | Frozen DINO backbone plus light heads: geometric place recognition ("where am I"), segmentation, and a projector that makes those features language-searchable in the Fusion Embedding space. |

### Engram — the memory layer

The open cross-modal memory layer for physical AI, built on Fusion Embedding. Index a robot's video,
audio, motion, and touch into one embedding space on a shared clock, then search and reason about it
in plain language.

```
pip install engram-robomem
```

Code: [Eximius-Labs/engram](https://github.com/Eximius-Labs/engram) · [PyPI](https://pypi.org/project/engram-robomem) · [Playground](https://www.eximiuslabs.com/playground)

### Efferent — the control layer

| Tool | Description |
|---|---|
| [efferent](https://github.com/Eximius-Labs/efferent) | Universal ONNX policy deployment. A policy trained in MuJoCo, Isaac Lab, Isaac Gym, or mjlab is an ONNX network plus an implicit contract; efferent makes that contract explicit and portable, joining policy and robot by joint name so a wrong name is a startup error rather than a fallen robot. `efferent doctor` probes the network itself to catch permuted joint order, world-vs-body frame errors, missing scales, and dead command dims before anything moves. |

```
pip install efferent
```

Code: [Eximius-Labs/efferent](https://github.com/Eximius-Labs/efferent) · [PyPI](https://pypi.org/project/efferent)

### Start here

- **Site:** [eximiuslabs.com](https://www.eximiuslabs.com)
- **Code:** [fusion-embedding](https://github.com/Eximius-Labs/fusion-embedding) · [fusion-perception](https://github.com/Eximius-Labs/fusion-perception) · [engram](https://github.com/Eximius-Labs/engram) · [efferent](https://github.com/Eximius-Labs/efferent) — Apache-2.0
- **Weights:** [huggingface.co/EximiusLabs](https://huggingface.co/EximiusLabs)
- **Technical report:** [arXiv:2607.18666](https://arxiv.org/abs/2607.18666)
