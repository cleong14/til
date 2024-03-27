# 2024-03-27 - TIL - LLM Quantisation Methods

Quantisation methods for LLMs.


**TL;DR**

> - *`Q4_K_M` is recommended for most LLMs **(medium, balanced quality)***
> - *`Q5_K_S` is recommended for low quality loss **(large, low quality loss)***
> - *`Q5_K_M` is recommended for very low quality loss **(large, very low quality loss)***


## Quantisation Methods

| Name | Quant method | Bits | Size | Max RAM required | Use case |
| --- | --- | --- | --- | --- | --- |
| [dolphin-2.2.1-mistral-7b.Q2_K.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q2_K.gguf) | Q2_K | 2 | 3.08 GB | 5.58 GB | smallest, significant quality loss - not recommended for most purposes |
| [dolphin-2.2.1-mistral-7b.Q3_K_S.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q3_K_S.gguf) | Q3_K_S | 3 | 3.16 GB | 5.66 GB | very small, high quality loss |
| [dolphin-2.2.1-mistral-7b.Q3_K_M.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q3_K_M.gguf) | Q3_K_M | 3 | 3.52 GB | 6.02 GB | very small, high quality loss |
| [dolphin-2.2.1-mistral-7b.Q3_K_L.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q3_K_L.gguf) | Q3_K_L | 3 | 3.82 GB | 6.32 GB | small, substantial quality loss |
| [dolphin-2.2.1-mistral-7b.Q4_0.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q4_0.gguf) | Q4_0 | 4 | 4.11 GB | 6.61 GB | legacy; small, very high quality loss - prefer using Q3_K_M |
| [dolphin-2.2.1-mistral-7b.Q4_K_S.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q4_K_S.gguf) | Q4_K_S | 4 | 4.14 GB | 6.64 GB | small, greater quality loss |
| [dolphin-2.2.1-mistral-7b.Q4_K_M.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q4_K_M.gguf) | Q4_K_M | 4 | 4.37 GB | 6.87 GB | medium, balanced quality - recommended |
| [dolphin-2.2.1-mistral-7b.Q5_0.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q5_0.gguf) | Q5_0 | 5 | 5.00 GB | 7.50 GB | legacy; medium, balanced quality - prefer using Q4_K_M |
| [dolphin-2.2.1-mistral-7b.Q5_K_S.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q5_K_S.gguf) | Q5_K_S | 5 | 5.00 GB | 7.50 GB | large, low quality loss - recommended |
| [dolphin-2.2.1-mistral-7b.Q5_K_M.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q5_K_M.gguf) | Q5_K_M | 5 | 5.13 GB | 7.63 GB | large, very low quality loss - recommended |
| [dolphin-2.2.1-mistral-7b.Q6_K.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q6_K.gguf) | Q6_K | 6 | 5.94 GB | 8.44 GB | very large, extremely low quality loss |
| [dolphin-2.2.1-mistral-7b.Q8_0.gguf](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF/blob/main/dolphin-2.2.1-mistral-7b.Q8_0.gguf) | Q8_0 | 8 | 7.70 GB | 10.20 GB | very large, extremely low quality loss - not recommended |

**Note**: the above RAM figures assume no GPU offloading. If layers are offloaded to the GPU, this will reduce RAM usage and use VRAM instead.


## Use Cases

- Quantisation methods for LLMs cheatsheet
- Helpful reference to use when selecting a quantisation method


## References

- [TheBloke/dolphin-2.2.1-mistral-7B-GGUF · Hugging Face](https://huggingface.co/TheBloke/dolphin-2.2.1-mistral-7B-GGUF#explanation-of-quantisation-methods)

