# He Xiao

**Applied AI · Forward-deployed engineering · AI infrastructure** · London

I take AI systems from "works in a demo" to "runs in a real environment and can be checked". Most of my work sits where a model meets messy operations: a supercomputer that rejects the obvious job script, a shop agent that must not refund the wrong order, a planning dataset nobody has mapped for infrastructure use.

A pattern you will see in every repo below: **the model proposes, deterministic code decides, and every output records where it came from.**

## Selected work

| Project | What it shows | Status |
|---|---|---|
| **vLLM on JUPITER** (case study below) | Brought up LLM serving on GH200 nodes of an ARM supercomputer through Slurm and Apptainer, with every image, model and script pinned by hash | First reproducible inference job passed; benchmarks next |
| **[LondonZero feasibility agent](https://github.com/HXIAOSHAW/londonzero_feasibility-agent)** | Six open London datasets → radius-filtered evidence → rule-based feasibility → optional Nemotron note that cannot overwrite the deterministic result. RAG, guardrails, provenance, Streamlit UI | Hackathon build, my component of a team project |
| **[MessagePilot AI](https://github.com/HXIAOSHAW/MessagePilot-AI)** | WhatsApp messages → orders, PayPal checkout and refunds. The LLM classifies a complaint; the backend enforces the refund policy and escalates the rest to a human | Cursor Hackathon 2026, team build (7 of 9 commits mine) |
| **[PLD Datahub Explorer](https://github.com/HXIAOSHAW/pld-datahub-explorer)** | Probed the Planning London Datahub API across 7 indices and surfaced 147 planning records relevant to data-centre and energy infrastructure, as an input for site screening | Exploratory; heuristic scoring, not a validated model |

Most of my infrastructure work belongs to my employer and is not public.

### Case study: vLLM on a European supercomputer

JUPITER is the EuroHPC exascale system in Jülich. Getting a model server to answer one prompt there is not a `pip install`: ARM (aarch64) nodes, Slurm scheduling, containers only through Apptainer, certificate plus TOTP access, and a billing model where mistakes cost node-hours.

What I did:
- Secured a EuroHPC research allocation and set up access, storage and a pinned vLLM container built for aarch64.
- Before spending GPU time, I staged a CUDA numeric self-test. Its dry run showed that the standard GPU request syntax is rejected on this cluster, and the real run surfaced how GPU requests are actually allocated and billed. Both are documented with logs.
- A preflight check caught a version-string mismatch inside the container *before* any GPU time was wasted on a broken server. Fixed once, resubmitted once.
- Result: a first reproducible vLLM inference job on JUPITER, with every file in the run verifiable by SHA-256.

## Contact

[LinkedIn](https://www.linkedin.com/in/dr-he-xiao/)
