# Rehearsal run

What this is: a cold, end-to-end workout of the bot team's change pipeline against a
throwaway public repo (`deyndev/studio-rehearsal-1031`). Every gate is executed
literally, on a repo nobody depends on, so the gate itself — not the content — is what
is being tested.

## The path this run exercises

1. **Branch** — `feat/rehearsal-docs`, cut off an up-to-date `main`. Nothing is ever
   committed to `main` directly.
2. **PR** — opened against `main` with a body quoting the author's own `lint`,
   `typecheck` and `test` exit codes verbatim. The author's exit codes are evidence,
   not a gate: the reviewer re-runs all three independently.
3. **Review gate** — branch protection on `main` requires one approving review and
   `enforce_admins` is on. The review is given by the reviewer account, never by the
   author. `--admin` is not used; a standing request-changes cannot be bypassed.
4. **Queued squash merge** — `gh pr merge <n> --auto --squash`. Auto-merge queues the
   PR and GitHub squash-merges it once the review gate is satisfied. `--auto` is the
   only merge command run. Its silence on exit 0 is confirmed by re-reading the PR
   state: armed means `state: OPEN` **and** a non-null `autoMergeRequest`.

## Result of these docs

The docs added by this run are themselves the payload, so the path is exercised
end-to-end with a real, reviewable diff. `docs/REHEARSAL-RUN.md` and the `##
Rehearsal` pointer in `README.md` are the only content changes; nothing in the repo's
scope is invented here.
