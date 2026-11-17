# Evidence & project status

[Project](../README.md) · [Walkthrough](demo.md)

This presentation was assembled on **17 November 2026** from the existing `cvut_mle_server` materials and the related chat **“Running AI on Servers”**, including terminal output from October 2026. Chat guidance alone is not treated as proof that a step succeeded. No fresh cluster deployment or performance test was run for this showcase.

| Claim | Evidence reviewed | Interpretation |
| --- | --- | --- |
| Slurm, one-node GPU allocation and Hermes launch settings | `poznamky.txt` | A documented setup recipe; each command is not independently verified by its own output. |
| Reachable Hermes model-list endpoint | `webui.txt`: saved authenticated response with model ID `hermes` and owner `vllm` | API discovery worked in the recorded session. This endpoint alone does not prove a generated chat response. |
| Generation activity | User-pasted historical vLLM logs in the related chat | Generation was active in that session. The log samples are not a controlled benchmark. |
| Open WebUI installation | Successful installation output in `webui.txt` | Client environment installed; browser interaction and tool-choice handling remain unverified. |
| Two-node model preparation | Download completion output for the same model revision on both nodes in the chat | Model preparation completed on two nodes. |
| Two-node serving | Subsequent traceback reporting missing `libcudart.so.13` | Captured startup failed; no later successful run is established in the reviewed material. |

The source notes and the chat describe different sessions. Context limits and installation approaches are therefore identified separately rather than combined into one supposedly reproduced configuration. The file `testovani_hermes.txt` is a saved model-answer example, not an independently scored quality evaluation.

## Authorship and boundaries

Jiří Doležal performed the user-level deployment work on existing university infrastructure, using AI-assisted troubleshooting. This case study does not claim hardware construction, ownership of the cluster, system-wide administration, model training or fine-tuning.

The public showcase contains a curated summary. Raw chats, personal correspondence, internal hosts, usernames, private network addresses and authentication material are omitted. Original source uploads were preserved when supplemental documentation was added.

## Technical references

These references explain the tools; they are not evidence that this particular deployment succeeded.

- [Slurm overview](https://slurm.schedmd.com/overview.html)
- [Hermes-4-70B model card](https://huggingface.co/NousResearch/Hermes-4-70B)
- [vLLM 0.10.0 distributed serving](https://docs.vllm.ai/en/v0.10.0/serving/distributed_serving.html)
- [Open WebUI: connecting vLLM](https://docs.openwebui.com/getting-started/quick-start/connect-a-provider/starting-with-vllm/)
