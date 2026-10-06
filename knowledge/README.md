# Knowledge

Material DevOps Agent reads when it reviews, and can cite in its findings: checklists, data-model notes, past
incidents, conventions this codebase follows.

- Write Markdown files here, one topic each (for example `checklist.md`, `data-model.md`).
- A review reads at most 20 files / 64 KB in total, in path order; files beyond that are listed by path only.
- The agent reads the files as they are on the default branch when the review starts, and records that commit.
