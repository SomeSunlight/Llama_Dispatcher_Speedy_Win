# Llama_Dispatcher – Instance: Speedy_Win

This repository contains the versioned Windows configuration of the **Speedy_Win**
instance for [Llama_Dispatcher](https://github.com/SomeSunlight/Llama_Dispatcher).

The corresponding WSL runtime is intentionally a separate instance/repository
(\`Speedy_WSL\`) with its own machine GUID and metrics history.

## Content

| Directory / File | Description |
|---|---|
| \`instance.yaml\` | Machine GUID and nickname of this Windows instance |
| \`profiles/\` | YAML profiles with model-relative paths and llama.cpp parameters |
| \`ensembles/\` | Model/alias compositions |
| \`engines/\` | Windows CUDA engine defaults |

Runtime-generated data does **not** belong to the versioned instance configuration:

- \`data/metrics.db\` is local live telemetry;
- generated router presets such as \`data/3090_models.ini\` are recreated locally;
- SQLite WAL/SHM files are local runtime state.

Historical measurements can later be published as deliberate, consistent SQLite
snapshots rather than by versioning the live database.

## Portable model paths

Profiles use \`\${LLAMA_MODEL_ROOT}\` instead of embedding a concrete Windows model root:

\`\`\`yaml
common:
  m: "\${LLAMA_MODEL_ROOT}/gemma-4-26B-A4B-it-qat-UD-Q4_K_XL.gguf"
\`\`\`

The concrete root is supplied at runtime with \`--model-root\`. The optional
\`LLAMA_MODEL_ROOT\` process environment variable remains only a Dispatcher fallback.

## Engine runtime paths

The \`bin_dir\` values in \`engines/*.yaml\` are Windows defaults for direct/manual use.
A managed launcher may override them explicitly with \`--bin-dir\`, so the profiles do
not depend on those filesystem paths.

Speedy currently needs no explicit GPU-selection environment variable. If such
backend-specific process environment is required later, it belongs in the engine
configuration rather than in shell startup instructions.

## Setup in a Dispatcher checkout

\`\`\`bash
git clone https://github.com/SomeSunlight/Llama_Dispatcher.git
cd Llama_Dispatcher
git clone https://github.com/SomeSunlight/Llama_Dispatcher_Speedy_Win.git instances/Speedy_Win
uv sync
\`\`\`

The existing Windows machine GUID in \`instance.yaml\` is intentionally preserved.
Do not reuse it for \`Speedy_WSL\`.

## Usage

\`\`\`bash
uv run src/dispatcher.py serve \\
  --ensemble 3090 \\
  --instance Speedy_Win \\
  --bin-dir C:/path/to/llama.cpp/bin \\
  --model-root C:/AI_Models/LLM/GGUF_Raw
\`\`\`

## License

MIT.
