# NEIGHBOR

Research materials for **NEIGHBOR: Aligning Service Behaviour and Evidence Use in Community-Facing LLM Agents**. NEIGHBOR combines LoRA-trained service behaviour with document retrieval and database tools.

| File | Contents |
| --- | --- |
| [Dataset](data/sft_examples.jsonl) | 500 de-identified SFT examples translated into English |
| [Data card](data/DATA_CARD.md) | Source, format, and usage notes |
| [Evaluation protocol](docs/EVALUATION_PROTOCOL.md) | Historical scoring rules and aggregate results |
| [Training setup](training/README.md) | LoRA settings and reproduction limits |

The examples originate from the Chinese V1 SFT dataset of 7,824 records; questions matching the 300-query test set were excluded. This package contains only their AI-generated English translations. They are training examples, not an English benchmark, and source answers have not been independently fact-checked.

Authors: Zongyou Yang, Yinghan Hou, Xiaokun Yang. Correspondence: `yangxk@bupt.cn`.

Project-owned contributions are licensed under [CC BY-NC 4.0](LICENSE): noncommercial research and adaptation are permitted, with attribution when sharing; commercial use is not licensed. See [license scope](LICENSE_STATUS.md) for the third-party source-text exclusions and outstanding redistribution review.
