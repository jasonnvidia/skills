## Description: <br>
Finds and installs relevant NVIDIA agent skills from the live NVIDIA skills catalog. Uses stable NVIDIA product and taxonomy categories as the implicit trigger surface, then checks the remote catalog for current skill-level matches. <br>

This skill is ready for commercial/non-commercial use after NVIDIA signing and release validation. <br>

## Owner
NVIDIA <br>

### License/Terms of Use: <br>
CC-BY-4.0 <br>

## Use Case: <br>
Developers, researchers, and operators who are working in NVIDIA-adjacent areas and may benefit from an NVIDIA skill that is not installed yet. The skill routes from broad user intent such as GPU acceleration, Decision Optimization, Physical AI, Vision AI, Training AI, Inference AI, Data Science on GPUs, Quantum, and accelerated infrastructure to live catalog lookup and installation guidance. <br>

### Deployment Geography for Use: <br>
Global <br>

## Known Risks and Mitigations: <br>
Risk: Over-triggering could interrupt generic software tasks that use broad words such as route, optimize, deploy, AI, data science, or infrastructure. <br>
Mitigation: The skill requires NVIDIA, GPU/accelerated-computing, or distinctive catalog intent signals before recommending a skill. Negative eval cases cover common false positives. <br>

Risk: Recommending stale or renamed skills could frustrate users or install the wrong capability. <br>
Mitigation: The skill instructs agents to query the live NVIDIA skills catalog before naming a specific install target and treats the local taxonomy reference only as fallback guidance. <br>

Risk: Installing a skill changes the user's agent behavior. <br>
Mitigation: The skill asks for explicit user approval before running `npx skills add`. <br>

## Reference(s): <br>
- [NVIDIA Skills Catalog](https://github.com/NVIDIA/skills) <br>
- [NVIDIA Skills on build.nvidia.com](https://build.nvidia.com/skills) <br>
- [skills.sh grouping config](https://raw.githubusercontent.com/NVIDIA/skills/main/skills.sh.json) <br>
- [Taxonomy Routing Reference](references/taxonomy-routing.md) <br>

## Skill Output: <br>
**Output Type(s):** [Skill recommendation, installation instructions, clarification question] <br>
**Output Format:** [Markdown with inline bash code blocks] <br>
**Output Parameters:** [1D] <br>
**Other Properties Related to Output:** [No files or external systems are modified unless the user approves installation.] <br>

## Evaluation Tasks: <br>
Evaluation dataset covers positive discovery for vehicle routing, GPU pandas acceleration, OpenUSD optimization, Dynamo/KV-aware routing, DICOM workflows, CAD-to-SimReady, and multi-GPU LLM training, plus negative cases for Express routes, React performance, generic Kubernetes deployment, ordinary video editing, and generic Python refactoring. <br>

## Evaluation Metrics Used: <br>
Reported benchmark dimensions: <br>
- Discoverability: Checks that the skill activates for stable NVIDIA taxonomy/product signals. <br>
- False-positive avoidance: Checks that generic route, optimize, deploy, video editing, and refactor tasks do not trigger NVIDIA skill recommendations. <br>
- Correctness: Checks that recommendations are based on live catalog lookup before naming a skill. <br>
- Safety: Checks that installation is proposed but not run without explicit user approval. <br>
- Efficiency: Checks that the skill does not mirror the full remote catalog in context. <br>

## Skill Version(s): <br>
1.0.0 (source: frontmatter/catalog submission) <br>

## Ethical Considerations: <br>
NVIDIA believes Trustworthy AI is a shared responsibility and has established policies and practices to enable development for a wide array of AI applications. When downloaded or used in accordance with applicable terms of service, developers should work with their internal team to ensure this skill meets requirements for the relevant industry and use case and addresses unforeseen product misuse. <br>

(For Release on NVIDIA Platforms Only) <br>
Please report quality, risk, security vulnerabilities or NVIDIA AI Concerns [here](https://app.intigriti.com/programs/nvidia/nvidiavdp/detail). <br>
