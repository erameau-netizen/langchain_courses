# notebooks_open_source

The open-source (Ollama cloud) recode of [`openai_agentic_ai_course`](../openai_agentic_ai_course/),
as notebooks instead of plain scripts.

[`open_source_agentic_ai_course`](../open_source_agentic_ai_course/) and
[`tools_and_agent`](../tools_and_agent/) already contain this same material as standalone `.py`
scripts (see each folder's own README for the full "what changed vs. the original course"
writeup). This folder puts the *same* lessons - reusing those folders' `common.py`, `tracing.py`
and `local_embeddings.py` rather than duplicating them - back into the small-cell,
markdown-narrated notebook format `openai_agentic_ai_course` uses, so they read the same way the
original DeepLearning.AI course notebooks do.

## Layout

Mirrors `openai_agentic_ai_course`'s two LangChain courses exactly (subfolder names and `L1`..`L6`
filenames match):

```
02-LangChain-for-LLM-Application-Development/   <- recodes open_source_agentic_ai_course
    L1-Model_prompt_parser.ipynb
    L2-Memory.ipynb
    L3-chains.ipynb
    L4-QnA.ipynb
    L5-Evaluation.ipynb
    L6-Agents.ipynb
03-Functions-Tools-and-Agents-with-LangChain/   <- recodes tools_and_agent
    L1-openai_functions_student.ipynb
    L2-lcel-student.ipynb
    L3-function-calling-student.ipynb
    L4-tagging-and-extraction-student.ipynb
    L5-tools-routing-apis-student.ipynb
    L6-functional_conversation-student.ipynb
```

`01-AI-Agents-in-LangGraph` and `04-Long-Term-Agentic-Memory-with-LangGraph` (the other two
courses under `openai_agentic_ai_course`) have no open-source recode yet, so there's nothing to
mirror them here.

## Running these

Each notebook's first code cell adds the matching script folder
(`open_source_agentic_ai_course/` or `tools_and_agent/`) to `sys.path` so it can `import common`
/ `tracing` / `local_embeddings` from there, and reads data files (where used) from that folder's
`data/` directory - nothing is copied, so a fix to `common.py` in one place benefits both the
scripts and these notebooks.

1. Open a notebook in VS Code / Jupyter and select the repo's `.venv` as the kernel
   (`Python 3 (ipykernel)` - it already has everything in
   [`requirements.txt`](../requirements.txt), including `ipykernel`, installed).
2. Make sure the repo-root `.env` has `OLLAMA_MODEL` / `OLLAMA_BASE_URL` / `OLLAMA_API_KEY` set
   (same three variables `src/model.py` and both script folders use).
3. Run cells top to bottom. **These notebooks ship unexecuted** - no outputs are saved - so you
   see your own model's real responses rather than a stale transcript.
4. Every `.invoke()` / `.batch()` / `.stream()` call passes `config=traced("run name")`, so each
   run shows up in the Langfuse dashboard (`LANGFUSE_*` vars in the same `.env`) - filter by
   trace name (e.g. `L3:`, `L5:`) to see a given notebook's calls.

## What's different from the scripts

Nothing behavioral - this is the same code, just split into small, individually-runnable cells
with markdown commentary between sections (matching `openai_agentic_ai_course`'s granularity)
instead of one top-to-bottom script with comment-banner sections. If you want the "run the whole
lesson in one go from a terminal" form, or a deeper dive into *why* each substitution was made
(e.g. why embeddings are a local TF-IDF implementation instead of `OllamaEmbeddings`, or why
`tool_choice` is a no-op on Ollama), see the source scripts and their folder READMEs:
[`open_source_agentic_ai_course/README.md`](../open_source_agentic_ai_course/README.md) and
[`tools_and_agent/README.md`](../tools_and_agent/README.md).
