# WORK_IN_PROGRESS.md — Active Task Tracking Template

**CHECK THIS FILE EVERY CYCLE BEFORE DOING ANYTHING ELSE.**

---

## How to Process This File

### Step 1: Is the task still active?
```
Check:
- Is "Current Task" section populated? If empty → no active task, proceed to sync
- Is Status = COMPLETE? If yes → move to Completed, proceed to sync
- Is Status = ABANDONED? If yes → clear it, proceed to sync
- Has it been >7 days with no progress? → Evaluate if still relevant
```

### Step 2: Where did we leave off?
```
Read the "Progress Log" section (newest entries at top):
- What was the LAST action taken?
- What was identified as NEXT ACTION?
- Are there any BLOCKERS noted?
```

### Step 3: Resume from NEXT ACTION
```
Don't re-read everything. Don't start over. 
Execute the specific NEXT ACTION listed.
After completing it, update:
- Add entry to Progress Log
- Update NEXT ACTION to the new next step
- Update Status if changed
```

### Step 4: Update before ending cycle
```
Before ending your cycle, ALWAYS update:
- Progress Log (what you did)
- NEXT ACTION (what comes next)
- Status (if changed)
- Completion Criteria (check boxes if done)
```

### Step 5: Capture Investigation Context (CRITICAL)
```
If you investigated/analyzed something, capture it in the task!
The NEXT ACTION alone is NOT enough. Include:

1. ROOT CAUSE ANALYSIS:
   - Flow that causes the bug (numbered steps)
   - Specific file paths and function names
   - Why the current code fails

2. IMPLEMENTATION PLAN:
   - Exact files to modify
   - What each change does (pseudocode OK)
   - Edge cases to handle
   - Test assertions (what to check, not just "add test")

3. CODE LOCATIONS:
   - File paths you discovered
   - Function names you found
   - Any offsets, line numbers, constants

Why? If you get interrupted, the NEXT agent shouldn't have to
re-investigate everything. They should be able to pick up your
analysis and implement directly.

BAD:
  NEXT ACTION: Implement Option A

GOOD:
  NEXT ACTION: Implement Option A
  
  ROOT CAUSE: install.ts embeds token in plist EnvironmentVariables,
  but lifecycle.ts restart() doesn't check for drift.
  
  FILES TO MODIFY:
  - src/cli/daemon-cli/lifecycle.ts: Add checkTokenDrift() before restart
  - Parse ~/Library/LaunchAgents/ai.openclaw.gateway.plist
  - Compare with config token from existing loader
  
  EDGE CASES:
  - Plist doesn't exist → skip (not LaunchAgent install)
  - Parse fails → warn but don't block restart
  
  TEST: Mock plist with token A, config token B, assert warning logged
```

---

## Current Task

**Task:** [Brief description]
**Started:** [Date]
**Status:** [RESEARCHING | DRAFTING | AWAITING_RESPONSE | BLOCKED | COMPLETE | ABANDONED]

### Completion Criteria
- [ ] [First criterion]
- [ ] [Second criterion]
- [ ] [Third criterion]

### Context
[What is this task about? Link to source if external.]

### Progress Log
[Newest entries at top]

[YYYY-MM-DD HH:MM] [Action taken]

### NEXT ACTION
[Specific next step to take]

### Blockers
[Any blocking issues - if none, delete this section]

---

## Completed Tasks

[Move completed tasks here with summary of outcome]

---

## Task Lifecycle Reference

### Statuses
| Status | Meaning | Action |
|--------|---------|--------|
| RESEARCHING | Gathering information | Continue research per NEXT ACTION |
| DRAFTING | Writing proposal/code | Complete the draft |
| AWAITING_RESPONSE | Waiting on external input | Check if response received |
| BLOCKED | Cannot proceed | Check if blocker resolved |
| COMPLETE | All criteria met | Move to Completed section |
| ABANDONED | No longer relevant | Clear and note why |

### Staleness Check
If task has no Progress Log updates for >3 days:
1. Is it still relevant? (Check with user if unclear)
2. If yes → add note explaining delay, continue
3. If no → mark ABANDONED with reason

### Starting New Tasks
Only add new task to Current Task section when:
1. Current Task is COMPLETE or ABANDONED
2. OR Current Task is BLOCKED and new task is higher priority
3. Always note if interrupting a blocked task
