markdown# Meeting Recording to Monday.com Task Automation Guide - WarmUp Edition

## Overview
This guide explains how to automatically process meeting transcripts from Notion and create actionable tasks in Monday.com using Claude with MCP integrations.

---

## Team Structure

**Partners & Strategists:**
- Deisy - Partner & Team Strategist
- Mike - Partner & Team Strategist

**GTMEs (Go-To-Market Execution):**
- Paula
- Josh
- Yasmin

**BDR (Business Development Representative):**
- Mery - Cold calling specialist

---

## Client Ownership

**Deisy's Clients:**
- UBT
- Paragon (Paragon Events)
- Numina
- Braden (BradenIT)
- XcelLabs
- Crede
- VAF
- Coya

**Mike's Clients:**
- All other clients (HG Insights, Kelly Schwedland, Sustainment, etc.)

---

## Required Claude Integrations

Before using this workflow, ensure these integrations are enabled in Claude Settings → Integrations:

1. **Notion** - To access meeting transcripts
2. **Monday.com** - To create and manage tasks

---

## Setup Instructions for Team Members

Before you can use this automated workflow, each team member needs to set up their Claude account with the required integrations.

### Step 1: Connect Notion to Claude
1. Go to Claude.ai and log in
2. Click on your profile (bottom left) → **Settings**
3. Navigate to **Integrations**
4. Find **Notion** and click **Connect**
5. Authorize Claude to access your Notion workspace
6. Grant access to the workspace containing meeting recordings

### Step 2: Connect Monday.com to Claude
1. In Claude Settings → **Integrations**
2. Find **Monday.com** and click **Connect**
3. Authorize Claude to access your Monday.com account
4. Ensure access to all client boards you work with

### Step 3: Verify Access to This Guide
Since this repository is public, Claude can access it directly without connecting GitHub. Simply provide Claude with the guide URL when running the workflow.

**Verification:** Once integrations are connected, test by asking Claude:
```
"Can you access my Notion workspace and Monday.com boards?"
```

---

## How to Execute the Workflow

### Daily Command

Each workday, just say to Claude:
```
Process this week's meeting recordings
```

**What Claude Will Do:**
1. Read this guide from GitHub
2. Search Notion for client meeting transcripts from current week (Monday through today)
3. Filter out meetings already marked "Processed" in Notion
4. Identify meetings for Deisy's clients only
5. Extract WarmUp team tasks (exclude client tasks)
6. Check Monday.com for duplicate tasks (last 7 days)
7. Create new tasks with "Review" status
8. Assign based on task type and meeting participants
9. Mark processed Notion pages with "Processed" checkbox
10. Report what was created

**Expected Time:** 2-5 minutes depending on number of meetings

**Best Time to Run:** Anytime during the workday - suggested around noon after morning meetings are transcribed

### Processing a Specific Meeting

If you need to process a single meeting outside the normal workflow:
```
Process this Notion meeting transcript: [paste Notion link]
Follow the guide's rules for task extraction and creation.
Mark it as processed when done.
```

---

## Advanced: Fully Automated Execution with Make.com

For completely hands-off automation, you can set up a Make.com scenario to trigger Claude daily.

### Overview
- **Trigger:** Schedule (daily at preferred time)
- **Action:** HTTP request to Claude API
- **Result:** Tasks created automatically without manual intervention

### Prerequisites
- Active Make.com account (WarmUp already uses this)
- Anthropic API key (available at console.anthropic.com)
- Claude API access (same integrations as web interface)

### Make.com Scenario Structure

**Module 1: Schedule**
- Trigger: Every day at your preferred time (e.g., 12:00 PM EST)
- Days: Monday-Friday (exclude weekends)

**Module 2: HTTP Request to Claude API**
- URL: `https://api.anthropic.com/v1/messages`
- Method: POST
- Headers:
```json
  {
    "x-api-key": "[Your Anthropic API Key]",
    "anthropic-version": "2023-06-01",
    "content-type": "application/json"
  }
```
- Body:
```json
  {
    "model": "claude-sonnet-4-20250514",
    "max_tokens": 4096,
    "messages": [
      {
        "role": "user",
        "content": "Read the meeting recordings guide from https://github.com/deisy-warmup/meetingrecordings/blob/main/Warmup-meeting-recordings-guide.md and execute the workflow. Process this week's meeting recordings from Notion and create tasks in Monday.com following all the rules in the guide."
      }
    ]
  }
```

**Module 3: Parse Response (Optional)**
- Extract confirmation of tasks created
- Send notification to Slack or email

### Setting Up Make.com Automation

1. **Get Anthropic API Key:**
   - Go to console.anthropic.com
   - Create new API key
   - Copy and save securely

2. **Create Make.com Scenario:**
   - New Scenario → Add Schedule module
   - Set to weekdays, your preferred time
   - Add HTTP module with Claude API request
   - Test the scenario

3. **Enable and Monitor:**
   - Turn on the scenario
   - Check logs daily for first week
   - Review Monday.com tasks in "Review" status

**Note:** API usage will incur costs based on Anthropic's pricing. Monitor your usage at console.anthropic.com.

---

## How It Works

### 1. Meeting Recording
- Record client meetings in Notion by pressing the meeting transcription button
- Notion will create a transcript page with a title like:
  - "UBT Onboarding w/ Deisy @Tuesday 9:45 AM"
  - "Weekly Check In: XcelLabs // WarmUp @Tuesday 12:30 PM"

### 2. Time Window & Duplicate Prevention

**Current Week Only:**
- Claude only processes meetings from Monday of the current week through today
- Meetings from previous weeks are automatically ignored
- This prevents processing old meetings multiple times

**Processed Tracking:**
- After processing a meeting and creating Monday tasks, Claude adds a "Processed" checkbox property to the Notion page
- On subsequent runs, Claude skips any meetings already marked "Processed"
- This ensures meetings are never processed twice

**Reset Each Week:**
- The "Processed" checkbox remains on pages indefinitely
- Each Monday, the new week's meetings are unprocessed and will be handled
- Old meetings stay marked and are never re-processed

### 3. Claude Identifies Client Meetings

Claude searches Notion for meeting transcripts that:
- ✅ Are from current week (Monday through today)
- ✅ Do NOT have "Processed" checkbox marked
- ✅ Contain client names from Deisy's client list (matches variations intelligently: "Braden" = "BradenIT", "Paragon" = "Paragon Events")
- ✅ Have meeting titles with these client names

Claude ignores:
- ❌ Meetings from previous weeks
- ❌ Meetings already marked "Processed"
- ❌ Internal WarmUp meetings
- ❌ Meetings with other clients (Mike's clients)
- ❌ Meetings without client names in title

### 4. Task Extraction Rules

**What Gets Created:**
- ✅ Action items for WarmUp team members only
- ✅ Clear, specific deliverables with context
- ✅ Tasks with identifiable owners

**What Gets Ignored:**
- ❌ Client-side action items (e.g., "Client will send brand guidelines")
- ❌ General discussion points without actions
- ❌ Tasks that already exist in Monday (checked against last 7 days of Completed tasks)

### 5. Task Assignment Logic

Claude assigns tasks based on task type and meeting participants:

| Task Type | Assigned To | How Claude Decides |
|-----------|-------------|-------------------|
| Campaign setup/optimization | GTME | Identifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned. |
| Email/LinkedIn sequences | GTME | Identifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned. |
| Technical setup (Clay, Make.com, webhooks) | GTME | Identifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned. |
| Data enrichment/research | GTME | Identifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned. |
| Reporting/analytics | GTME | Identifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned. |
| Client strategy/planning | Deisy or Mike | Based on client ownership list |
| Cold calling/phone outreach | Mery (BDR) | Always assigned to BDR |

**GTME Assignment Rules:**
- ✅ If exactly ONE GTME (Paula, Josh, or Yasmin) is in the meeting → Assign GTME tasks to that person
- ❌ If MULTIPLE GTMEs are in the meeting → Leave GTME tasks unassigned for manual assignment
- ❌ If NO GTME is in the meeting → Leave GTME tasks unassigned for manual assignment

**Strategy Task Assignment:**
- For Deisy's clients → Assign to Deisy
- For all other clients → Assign to Mike

### 6. Task Properties

**Status:**
- All new tasks automatically set to "Review"

**Priority:**
- Default: Medium
- If meeting explicitly mentions "high priority", "urgent", or "critical" → Set to High
- Otherwise → Medium

**Due Date:**
- If specific date mentioned in meeting → Use that date
- If timeframe mentioned (e.g., "by end of week", "next Tuesday") → Calculate appropriate date
- If no due date mentioned → Default to Friday of current week
- Remember: Tasks due Friday or earlier = "This Week" group, After Friday = "Upcoming" group

**Assignee:**
- Determined by task type and meeting context (see Task Assignment Logic above)

### 7. Monday.com Board Structure

**Each client has their own board:**
- Board naming: "[Client Name] Tasks - [GTME Name]"
- Examples: "BradenIT Tasks - JOSH", "Coya Tasks - PAULA"

**Groups within each board:**
- **This Week** - Tasks due by Friday (2 days before end of week)
- **Upcoming** - Tasks due after Friday
- **Completed** - Finished tasks (Claude checks last 7 days for duplicates)

### 8. Duplicate Prevention

Before creating any task, Claude:
1. Checks if the Notion meeting page is already marked "Processed" (skip if yes)
2. Searches the Monday.com board for similar tasks
3. Checks "Completed" group for tasks completed in the last 7 days
4. Compares task descriptions to avoid creating duplicates
5. Only creates task if it's genuinely new

After creating tasks, Claude:
1. Adds "Processed" checkbox property to the Notion meeting page
2. This permanently marks the meeting as handled
3. Future runs will skip this meeting automatically

---

## Workflow Example

**Scenario:** Tuesday morning meeting with UBT, Josh (GTME) attending

1. **12:30 PM Tuesday:** You record the meeting in Notion
   - Notion creates: "UBT Onboarding w/ Deisy @Tuesday 12:30 PM"
   - Page does not have "Processed" checkbox yet

2. **3:00 PM Wednesday:** You run the workflow command
   - Claude searches Notion for current week's meetings
   - Finds UBT meeting from Tuesday (within current week)
   - Checks: No "Processed" checkbox ✓
   - Matches "UBT" from Deisy's client list ✓
   - Reviews transcript and extracts:
     - "Set up Clay table for UBT contact enrichment by end of week" → GTME task
     - "This is high priority - schedule follow-up strategy call for next week" → Deisy task
     - "UBT will provide access to their CRM by Friday" → Ignored (client task)

3. **Claude identifies meeting participants:**
   - Deisy present ✓
   - Josh (GTME) present ✓
   - Only one GTME, so tasks can be assigned

4. **Claude checks Monday.com "UBT" board:**
   - Searches "Completed" group (last 7 days)
   - No duplicate tasks found

5. **Claude creates tasks in "UBT" board:**
   - Task 1: "Set up Clay table for UBT contact enrichment"
     - Group: This Week (due Friday - mentioned "by end of week")
     - Assignee: Josh (only GTME in meeting)
     - Priority: Medium (default)
     - Status: Review
   
   - Task 2: "Schedule follow-up strategy call for next week"
     - Group: Upcoming (due next week)
     - Assignee: Deisy (client owner)
     - Priority: High (explicitly mentioned "high priority")
     - Status: Review

6. **Claude marks the Notion page:**
   - Adds "Processed" checkbox property to the meeting page
   - Checkbox is checked ✓
   - Meeting will be skipped in all future runs

7. **Thursday you run workflow again:**
   - Claude searches current week's meetings
   - Finds Tuesday's UBT meeting
   - Sees "Processed" checkbox is checked
   - Skips this meeting automatically
   - Only processes new meetings from Wednesday/Thursday

---

## Edge Cases & Special Situations

**Multiple GTMEs in meeting:**
- Example: Both Paula and Josh attend Coya meeting
- Result: All GTME tasks left unassigned in Monday
- Action: Manually assign tasks after reviewing

**Client name variation:**
- Example: Transcript says "Braden" but client list has "BradenIT"
- Result: Claude intelligently matches and processes normally
- Matches: "Paragon" = "Paragon Events", "Braden" = "BradenIT", "XCel" = "XcelLabs"

**Ambiguous due dates:**
- Example: "Get this done soon" or "ASAP"
- Result: Defaults to Friday of current week
- Action: Review and adjust manually if needed

**Mixed priority signals:**
- Example: "Important but not urgent"
- Result: Defaults to Medium unless "high priority", "urgent", or "critical" explicitly stated
- Action: Adjust priority in Monday if needed

**No clear task owner:**
- Example: "Someone needs to check on this"
- Result: Claude will attempt to assign based on task type, may leave unassigned if unclear
- Action: Manually assign during review

**Meeting from last week reappears:**
- Example: Old meeting page is moved or renamed
- Result: If "Processed" checkbox is present, it will still be skipped
- Action: If checkbox was removed, Claude may reprocess - manually mark as Processed

**Week starts on Sunday vs Monday:**
- This workflow uses Monday as week start
- Sunday meetings from previous week won't be processed
- Action: Manually process if needed using specific meeting command

---

## Troubleshooting

**Meeting transcript not found:**
- Verify client name is in the Notion page title
- Check that recording was completed (not just started)
- Ensure meeting is from current week (Monday - today)
- Verify meeting doesn't already have "Processed" checkbox
- Try manual processing with direct Notion link

**Wrong person assigned:**
- Check if correct GTME was identified in transcript speakers
- For strategy tasks, verify client is in correct ownership list
- Manually reassign in Monday if needed

**Duplicate tasks created:**
- May indicate task name/description varies significantly
- Check if previous task was in "Completed" group older than 7 days
- Check if Notion page somehow lost its "Processed" checkbox
- Mark as duplicate and delete in Monday

**Task in wrong group:**
- Verify due date interpretation from meeting notes
- Remember: Friday or before = "This Week", After Friday = "Upcoming"
- Manually move between groups as needed

**No tasks created from meeting:**
- All action items may have been client-side
- Meeting may have been informational only
- Check Notion transcript exists and is complete
- Verify client name matches Deisy's client list (with variations)
- Check if meeting was already processed (has "Processed" checkbox)

**Wrong priority assigned:**
- Claude looks for explicit mentions of "high priority", "urgent", "critical"
- Other urgency language may not trigger High priority
- Manually adjust in Monday after review

**Multiple GTMEs, but tasks assigned anyway:**
- Report to Deisy - may indicate speaker identification issue
- Manually verify and reassign if needed

**Claude can't access Notion/Monday:**
- Verify integrations are connected in Claude Settings
- Check permissions were granted during connection
- Try disconnecting and reconnecting the integration
- Ensure correct workspace/account is selected

**Meeting processed twice:**
- Check if "Processed" checkbox was manually removed from Notion page
- Verify checkbox property is still present and checked
- If duplicate tasks created, delete in Monday and ensure checkbox is present

**Can't find "Processed" checkbox in Notion:**
- The checkbox is a page property, not in the page content
- Look at the top of the page for properties section
- If missing, Claude will add it automatically on next processing

---

## Best Practices

1. **Clear action items in meetings:** State clearly "WarmUp will [do X]" vs "Client will [do Y]"

2. **Mention names:** Reference team members by name in meetings to help Claude assign correctly

3. **Due dates:** Mention specific timeframes in meetings ("by end of week", "by next Tuesday", "by Friday")

4. **Priority:** Explicitly say "this is high priority" or "this is urgent" for important tasks

5. **Review daily:** Check "Review" status tasks in Monday.com each afternoon

6. **Single GTME meetings:** When possible, have one GTME per client meeting to enable automatic assignment

7. **Run regularly:** Execute the workflow command at least once daily during the work week to stay current

8. **Don't remove "Processed" checkbox:** Leave the checkbox on Notion pages to prevent reprocessing

9. **Week boundaries:** Remember workflow resets each Monday - previous week's meetings won't be touched

10. **Provide feedback:** If Claude consistently misassigns or misinterprets, update this guide

11. **Test before full rollout:** Run manually for 1-2 weeks before setting up Make.com automation

12. **Monitor API usage:** If using Make.com automation, check Anthropic console for API costs

---

## Updating This Workflow

**To add a new client to Deisy's list:**
1. Update "Client Ownership" section above
2. Ensure Monday.com board exists for that client
3. Claude will automatically include in next workflow run

**To add a new team member:**
1. Update "Team Structure" section above
2. Update "Task Assignment Logic" if needed for their role
3. Add to appropriate Monday.com boards

**To change time window:**
1. Update "Time Window & Duplicate Prevention" section
2. Current setting: Current week (Monday - today)
3. Alternative: Could change to "last 2 days" or "yesterday only"
4. Communicate changes to team

**To modify client name matching:**
1. Document variations in "Client Ownership" section
2. Example: "Braden (BradenIT, Braden IT)"
3. Claude will match all variations

**To update task assignment rules:**
1. Modify "Task Assignment Logic" table
2. Add examples to "Workflow Example" if helpful
3. Communicate changes to team

**To manually reprocess a meeting:**
1. Open the Notion meeting page
2. Uncheck or remove the "Processed" checkbox
3. Run the workflow command
4. Meeting will be processed again

---

## Questions or Issues?

Contact Deisy for any questions about this workflow or to suggest improvements to the automation.

---

*Last Updated: February 7, 2026*  
*Version: 3.0*  
*Team: WarmUp*  
*Changes: Added current week filter and Notion "Processed" checkbox tracking to prevent duplicate processing*
