
I've found that even reseting context every step the executor seems to ignore and miss steps if they aren't laid out in the document (mainly archiving the completed feature), so I pulled all of that out into a specific new mode. 

## New Structure
- **Planner**: Creates the detailed feature planning documents.
- **Executor**: Executes the feature planned by the planner.
- **Archiver**: Archives the feature plan, along with the original feature prompt, and optionally any other additional files requested by the user.

### Notes
**Planner**
    - Added a rule so the planner creates a second document `feature-prompt.md` that contains the entire unchanged prompt that it used to create `feature-plan.md`.
    - Added a rule to always include linting, formatting, and pausing as the last 3 substeps in every step since the executor had trouble remembering to pause.
    - Changed date fetching to use PowerShell commands instead of searching the web. It was _really_ bad at getting the date correct.

**Executor**
    - Added rules to run linting, formatting, and then pause after every step. This was the original attempt at pausing, but it didn't work well. I figured to leave this here to increase the changes it stays in the context window.

**Archiver**
    - Asks you if there's any files you would like to archive along with `feature-plan.md` and `feature-prompt.md`. 
    - Create an archived file in the history directory, the prompt is always first, the plan is second, and then any additional files.
    - Deletes `feature-plan.md` and `feature-prompt.md` and asks you if it should also delete the additional files.