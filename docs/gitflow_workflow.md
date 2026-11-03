# Gitflow workflow

This document explains how the team organizes its work in the repository.

## 1. Branches

| Branch | Purpose | Who touches it |
| --- | --- | --- |
| `main` | Delivered versions. Protected: code only enters through a Pull Request with 1 approval. | Release only |
| `develop` | Integration of the work. It is the default branch and is also protected. | Pull Requests only |
| `feature/<student>/<module>` | One personal branch per task. Branches off `develop` and merges back into `develop`. | Its author |
| `release/v1.0` | Delivery preparation. Branches off `develop` and goes to `main`. | Both members |
| `hotfix/<topic>` | Urgent fix on `main`. | Whoever finds it |

## 2. Feature branch names

Format: `feature/student-name/module`, all lowercase with hyphens.

```
feature/cartagena/repo-kanban
feature/cartagena/registros-isa
feature/<member-b>/memoria-virtual
```

Each task is developed by its owner on their own branch, so the history shows who did each part.

## 3. Semantic commits

Format: `type(scope): short description (#issue)`

| Type | Used for |
| --- | --- |
| `feat` | a new feature |
| `fix` | fixing a bug |
| `docs` | documentation |
| `test` | tests |
| `chore` | setup and maintenance tasks |
| `refactor` | restructuring code without changing behavior |

Examples:

```
feat(cpu): 8-bit ALU with ZF, CF and SF flags (#7)
fix(mem): never pick page 15 as a victim (#12)
docs: initial README in Spanish and English (#1)
```

Rules: small, atomic commits (one change, one reason), messages that say what changed, and the issue number at the end.

## 4. Cycle for each task

1. Start from an up-to-date `develop`: `git checkout develop` and `git pull`.
2. Create the branch: `git checkout -b feature/<student>/<module>`.
3. Work with small, semantic commits.
4. Push the branch: `git push -u origin feature/<student>/<module>`.
5. Open a Pull Request against `develop` with `Closes #N` in the description.
6. Move the board card to **In Review**.
7. **The other member** reviews (*Files changed → Review changes → Approve*) and merges with **Merge pull request**.
8. The issue closes itself and moves to **Done**. The branch is deleted.

## 5. Kanban board

Columns: **Backlog**, **To Do**, **In Progress**, **In Review**, **Done**.

## 6. Labels

`setup`, `cpu`, `bus`, `mem`, `cache`, `io`, `asm`, `prog`, `ui`, `doc`, `qa`, `def` (epics) and `integrante-A`, `integrante-B` (owner).

## 7. Issue and branch split

| Branch | Owner | Issues |
| --- | --- | --- |
| `feature/cartagena/repo-kanban` | A | #1 |
| `feature/<member-b>/estructura-build` | B | #2 |
| `feature/cartagena/registros-isa` | A | #3, #4 |
| `feature/cartagena/unidad-control` | A | #5, #6, #7, #8 |
| `feature/<member-b>/memoria-virtual` | B | #10, #11, #12, #13 |
| `feature/<member-b>/caches` | B | #14, #15 |
| `feature/<member-b>/entrada-salida` | B | #16, #17 |
| `feature/cartagena/ensamblador` | A | #18, #19 |
| `feature/cartagena/programas-base` | A | #20 |
| `feature/cartagena/panel` | A | #9, #22, #24 |
| `feature/<member-b>/ejercicios` | B | #21, #23 |
| `feature/<member-b>/documentacion` | B | #25 |
| `feature/<member-b>/pruebas` | B | #26 |
| `release/v1.0` | A + B | #27 |

## 8. Release

```bash
git checkout develop && git pull
git checkout -b release/v1.0
# final adjustments, CHANGELOG
git push -u origin release/v1.0
gh pr create --base main --title "Release v1.0"
```

After it merges into `main`: tag `v1.0` and merge the changes back into `develop`.

## 9. Rules

- Nobody pushes directly to `main` or `develop`.
- Nobody approves their own Pull Request.
- Commits after the official repository closing date and time are not accepted.
