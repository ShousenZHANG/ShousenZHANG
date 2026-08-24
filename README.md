<div align="center">

**Building production LLM systems** — retrieval, evals, agents, and the backends that serve them.

<sub>
  <a href="https://www.joblit.tech/">Joblit</a>
  &nbsp;·&nbsp;
  <a href="https://eddyzhang.me/">Portfolio</a>
  &nbsp;·&nbsp;
  <a href="https://linkedin.com/in/eddy-shousen-zhang">LinkedIn</a>
  &nbsp;·&nbsp;
  <a href="mailto:eddy.zhang24@gmail.com">Email</a>
</sub>

</div>

## Open Source

Contributor to **[Haystack](https://github.com/deepset-ai/haystack)** — deepset's production RAG / LLM orchestration framework (26k+ ⭐):

- [#12438](https://github.com/deepset-ai/haystack/pull/12438) `fix` — `EmbeddingBasedDocumentSplitter` emitted a final chunk shorter than its documented `min_length`. Root-caused the forward-only merge loop, fixed it under the same `max_length` guard the loop already used, and locked it in with regression tests.
- [#12441](https://github.com/deepset-ai/haystack/pull/12441) `test` — brought `test/components/evaluators/` under the repository's mypy gate (19 errors → 0) as an increment of the typing campaign [#10396](https://github.com/deepset-ai/haystack/issues/10396), without changing what any test asserts.
