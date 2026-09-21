# Suggested teaching order

The two subfolders keep their original `openai_agentic_ai_course` numbering (`L1`..`L6` inside
each), but the two courses overlap enough - both build up LCEL, both build up tool-calling -
that going through each folder top to bottom back to back isn't the order that introduces
concepts before you need them. This is the order that does, worked out lesson by lesson.

Two deviations from "02 then 03, in file order" drive the whole list:

1. **LCEL itself is taught in 03-L2, not 02.** 02 starts using `prompt | model | StrOutputParser()`
   from its first lesson without explaining the pipe operator; 03-L2 is where `invoke`/`batch`/
   `stream`, `.bind()`, and `.with_fallbacks()` actually get taught from scratch. 03-L1 (raw
   `ollama` client, no LangChain) rides along in front of it - it's the "here's the pain LCEL
   solves" motivation.
2. **`02-L6` (Agents) uses tool-calling without explaining it.** `create_agent` hands the model a
   couple of `@tool`-decorated functions and the whole call/execute/respond loop "just works" -
   but what a tool call *is* at the wire level is 03-L1, how `bind_tools` turns a Pydantic model
   into that wire format is 03-L3, and the `@tool` decorator plus manually reading
   `message.tool_calls` to route is 03-L5. `02-L6` only stops feeling like magic once those have
   landed, so it moves to just before the very last lesson instead of sitting mid-course-02.

Everything else in 02 (`L1`-`L5`: prompts/parsers, memory, chains, RAG, evaluation) never touches
tool-calling, so it's unaffected and stays together, right after the LCEL primer.

## The order

| # | Notebook | Why here |
|---|----------|----------|
| 1 | [`03-Functions-Tools-and-Agents-with-LangChain/L1-openai_functions_student.ipynb`](03-Functions-Tools-and-Agents-with-LangChain/L1-openai_functions_student.ipynb) | Raw `ollama` client, no LangChain - shows function-calling at the wire level, and the manual pain LCEL is about to remove. |
| 2 | [`03-Functions-Tools-and-Agents-with-LangChain/L2-lcel-student.ipynb`](03-Functions-Tools-and-Agents-with-LangChain/L2-lcel-student.ipynb) | LCEL from scratch: `invoke`/`batch`/`stream`, `RunnableMap`, `.bind()`, `.with_fallbacks()`. Everything downstream assumes this. |
| 3 | [`02-LangChain-for-LLM-Application-Development/L1-Model_prompt_parser.ipynb`](02-LangChain-for-LLM-Application-Development/L1-Model_prompt_parser.ipynb) | Prompt templates and `with_structured_output` - no tool-calling involved. |
| 4 | [`03-Functions-Tools-and-Agents-with-LangChain/L4-tagging-and-extraction-student.ipynb`](03-Functions-Tools-and-Agents-with-LangChain/L4-tagging-and-extraction-student.ipynb) | Same primitive as the lesson right above it (`with_structured_output`) - reinforces it on a live Wikipedia article while it's fresh, before moving on. |
| 5 | [`02-LangChain-for-LLM-Application-Development/L2-Memory.ipynb`](02-LangChain-for-LLM-Application-Development/L2-Memory.ipynb) | Conversation history strategies - no tool-calling involved. |
| 6 | [`02-LangChain-for-LLM-Application-Development/L3-chains.ipynb`](02-LangChain-for-LLM-Application-Development/L3-chains.ipynb) | Chain composition (`RunnablePassthrough.assign`, the router chain) - builds on the LCEL primer from #2, no tool-calling involved. |
| 7 | [`02-LangChain-for-LLM-Application-Development/L4-QnA.ipynb`](02-LangChain-for-LLM-Application-Development/L4-QnA.ipynb) | RAG: vector store, retriever, LCEL RAG chain. |
| 8 | [`02-LangChain-for-LLM-Application-Development/L5-Evaluation.ipynb`](02-LangChain-for-LLM-Application-Development/L5-Evaluation.ipynb) | LLM-generated examples + LLM-as-judge grading, over the L4 RAG chain. |
| 9 | [`03-Functions-Tools-and-Agents-with-LangChain/L3-function-calling-student.ipynb`](03-Functions-Tools-and-Agents-with-LangChain/L3-function-calling-student.ipynb) | `bind_tools` with a Pydantic schema - tool-calling *in* LangChain, building on #1's wire-level explanation. |
| 10 | [`03-Functions-Tools-and-Agents-with-LangChain/L5-tools-routing-apis-student.ipynb`](03-Functions-Tools-and-Agents-with-LangChain/L5-tools-routing-apis-student.ipynb) | The `@tool` decorator properly explained, plus manually reading `message.tool_calls` to route - the exact loop `create_agent` automates next. |
| 11 | [`02-LangChain-for-LLM-Application-Development/L6-Agents.ipynb`](02-LangChain-for-LLM-Application-Development/L6-Agents.ipynb) | `create_agent` with tools (calculator, Wikipedia, a Python REPL, a custom tool) - the manual loop from #10, automated. No longer magic. |
| 12 | [`03-Functions-Tools-and-Agents-with-LangChain/L6-functional_conversation-student.ipynb`](03-Functions-Tools-and-Agents-with-LangChain/L6-functional_conversation-student.ipynb) | `create_agent` + a `checkpointer` for cross-turn memory - the capstone, combining #11's agent with #5's "why memory matters." |

## Note on #4's placement

`03-L4` (tagging and extraction) is placed early because it shares a primitive with `02-L1`
(`with_structured_output`), not because it needs tool-calling internals - it doesn't. The other
defensible spot for it is down with `03-L3`/`03-L5` (#9/#10), just to keep "the rest of course
03" together. Move it there if you'd rather group by course than by shared primitive.
