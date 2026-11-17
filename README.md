# AI Cluster — LLM Inference Setup

**Deploying a 70B language model on a shared university GPU cluster.**

[Architecture & walkthrough](docs/demo.md) · [Evidence & status](docs/evidence.md) · [All projects](https://github.com/Dolik64)

## What I set up

I configured an LLM inference environment on an existing CTU FEL teaching cluster: allocating compute resources with Slurm, preparing Python environments and model storage, serving **NousResearch/Hermes-4-70B** through **vLLM**, and accessing its OpenAI-compatible API from my laptop through an SSH tunnel. I also prepared a local Open WebUI client and explored a later two-node deployment.

My work covers the user-level software setup, resource requests, remote access and troubleshooting. The university provides the hardware, network and cluster administration.

## Technical scope

| Area | Work performed |
| --- | --- |
| Resource management | Slurm allocation requesting one node, 96 CPUs and 16 NVIDIA A16 GPU devices. |
| Model deployment | Hermes-4-70B weights, node-local scratch/cache and vLLM serving configuration. |
| Multi-GPU configuration | Documented BF16 setup with tensor parallelism 8 and pipeline parallelism 2 within one node. |
| Remote access | SSH forwarding through the login node; authenticated model-list request from the laptop. |
| Client integration | Local Open WebUI installation and connection preparation. |
| Further experiment | Same model revision downloaded to two nodes for a Qwen experiment; launch troubleshooting. |

The 16 devices refer to GPU devices visible to the runtime, not 16 physical accelerator boards. The TP8 × PP2 settings describe the documented single-node launch, not a verified two-node deployment.

## Recorded results

- **Hermes API responded:** a saved authenticated `/v1/models` response identifies the served model as `hermes`.
- **Inference activity was recorded:** historical vLLM logs show generation activity. No controlled throughput or latency benchmark is claimed.
- **Open WebUI was installed:** installation output is available; a complete browser chat session is not demonstrated in the reviewed records.
- **Two-node preparation completed:** model downloads finished on both nodes. The captured launch then failed with a missing `libcudart.so.13`; successful distributed inference is not established by those records.

This is a historical case study, not a continuously hosted public demo. The [walkthrough](docs/demo.md) explains the workflow; the [evidence table](docs/evidence.md) distinguishes terminal output from setup notes and plans.

**Stack:** Linux · Slurm · Python · CUDA · vLLM · Hugging Face Hub · SSH · Open WebUI · Docker

This showcase contains presentation documents and an architecture diagram. It does not include application source, executable deployment scripts, raw chats, credentials or internal connection details.
