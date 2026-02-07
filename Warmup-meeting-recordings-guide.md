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

### Manual Daily Execution (Recommended to Start)

Each workday, run this command in Claude:
```
Read the meeting recordings guide from 
https://github.com/deisy-warmup/meetingrecordings/blob/main/Warmup-meeting-recordings-guide.md

Search Notion for client meeting transcripts from yesterday.
Process transcripts following the guide rules and create tasks in Monday.com.
```

**Best Time to Run:** 12:00 PM EST daily (after morning meetings are transcribed)

**What Claude Will Do:**
1. Fetch and read this guide
2. Search your Notion for meeting transcripts with client names
3. Identify meetings for Deisy's clients only
4. Extract WarmUp team tasks (exclude client tasks)
5. Check Monday.com for duplicate tasks (last 7 days)
6. Create new tasks with "Review" status
7. Assign based on task type and meeting participants
8. Report what was created

**Expected Time:** 2-5 minutes depending on number of meetings

### Processing a Specific Meeting

If you need to process a single meeting outside the daily automation:
```
Read the meeting recordings guide from 
https://github.com/deisy-warmup/meetingrecordings

Process this Notion meeting transcript: [paste Notion link]
Follow the guide's rules for task extraction and creation.
```

---

## Advanced: Fully Automated Execution with Make.com

For completely hands-off automation, you can set up a Make.com scenario to trigger Claude daily.

### Overview
- **Trigger:** Schedule (daily at 12:00 PM EST)
- **Action:** HTTP request to Claude API
- **Result:** Tasks created automatically without manual intervention

### Prerequisites
- Active Make.com account (WarmUp already uses this)
- Anthropic API key (available at console.anthropic.com)
- Claude API access (same integrations as web interface)

### Make.com Scenario Structure

**Module 1: Schedule**
- Trigger: Every day at 12:00 PM EST
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
        "content": "Read the meeting recordings guide from https://github.com/deisy-warmup/meetingrecordings/blob/main/Warmup-meeting-recordings-guide.md and execute the daily workflow. Search Notion for yesterday's client meeting transcripts and create tasks in Monday.com following all the rules in the guide."
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
   - Set to weekdays, 12:00 PM EST
   - Add HTTP module with Claude API request
   - Test the scenario

3. **Enable and Monitor:**
   - Turn on the scenario
   - Check logs daily for first week
   - Review Monday.com tasks in "Review" status

**Note:** API usage will incur costs based on Anthropic's pricing. Monitor your usage at console.anthropic.com.

---

## Automation Schedule

**Daily at 12:00 PM EST:**
Claude automatically (if using Make.com) or manually triggered:
1. Searches Notion for new meeting transcripts from the previous day
2. Identifies client meetings for Deisy's clients only
3. Extracts WarmUp team action items
4. Creates tasks in the appropriate Monday.com board
5. Sets all new tasks to "Review" status

---

## How It Works

### 1. Meeting Recording
- Record client meetings in Notion by pressing the meeting transcription button
- Notion will create a transcript page with a title like:
  - "UBT Onboarding w/ Deisy @Tuesday 9:45 AM"
  - "Weekly Check In: XcelLabs // WarmUp @Tuesday 12:30 PM"

### 2. Claude Identifies Client Meetings
Claude searches Notion for meeting transcripts that contain:
- ✅ Client names from Deisy's client list (matches variations intelligently: "Braden" = "BradenIT", "Paragon" = "Paragon Events")
- ✅ Meeting titles with these client names

Claude ignores:
- ❌ Internal WarmUp meetings
- ❌ Meetings with other clients (Mike's clients)
- ❌ Meetings without client names in title

### 3. Task Extraction Rules

**What Gets Created:**
- ✅ Action items for WarmUp team members only
- ✅ Clear, specific deliverables with context
- ✅ Tasks with identifiable owners

**What Gets Ignored:**
- ❌ Client-side action items (e.g., "Client will send brand guidelines")
- ❌ General discussion points without actions
- ❌ Tasks that already exist in Monday (checked against last 7 days of Completed tasks)

### 4. Task Assignment Logic

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

### 5. Task Properties

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

### 6. Monday.com Board Structure

**Each client has their own board:**
- Board naming: "[Client Name] Tasks - [GTME Name]"
- Examples: "BradenIT Tasks - JOSH", "Coya Tasks - PAULA"

**Groups within each board:**
- **This Week** - Tasks due by Friday (2 days before end of week)
- **Upcoming** - Tasks due after Friday
- **Completed** - Finished tasks (Claude checks last 7 days for duplicates)

### 7. Duplicate Prevention

Before creating any task, Claude:
1. Searches the Monday.com board for similar tasks
2. Checks "Completed" group for tasks completed in the last 7 days
3. Compares task descriptions to avoid creating duplicates
4. Only creates task if it's genuinely new

---

## Workflow Example

**Scenario:** Tuesday morning meeting with UBT, Josh (GTME) attending

1. **12:30 PM Tuesday:** You record the meeting in Notion
   - Notion creates: "UBT Onboarding w/ Deisy @Tuesday 12:30 PM"

2. **12:00 PM Wednesday (EST):** Claude's daily automation runs (or you trigger manually)
   - Searches Notion for new transcripts
   - Finds UBT meeting (matches "UBT" from Deisy's client list)
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

6. **You review tasks:**
   - Check tasks in "Review" status
   - Adjust due dates, descriptions, or assignments if needed
   - Change status to move forward

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

---

## Troubleshooting

**Meeting transcript not found:**
- Verify client name is in the Notion page title
- Check that recording was completed (not just started)
- Ensure meeting happened within last 24 hours
- Try manual processing with direct Notion link

**Wrong person assigned:**
- Check if correct GTME was identified in transcript speakers
- For strategy tasks, verify client is in correct ownership list
- Manually reassign in Monday if needed

**Duplicate tasks created:**
- May indicate task name/description varies significantly
- Check if previous task was in "Completed" group older than 7 days
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

---

## Best Practices

1. **Clear action items in meetings:** State clearly "WarmUp will [do X]" vs "Client will [do Y]"

2. **Mention names:** Reference team members by name in meetings to help Claude assign correctly

3. **Due dates:** Mention specific timeframes in meetings ("by end of week", "by next Tuesday", "by Friday")

4. **Priority:** Explicitly say "this is high priority" or "this is urgent" for important tasks

5. **Review daily:** Check "Review" status tasks in Monday.com each afternoon after the 12pm EST automation runs

6. **Single GTME meetings:** When possible, have one GTME per client meeting to enable automatic assignment

7. **Provide feedback:** If Claude consistently misassigns or misinterprets, update this guide

8. **Test before full rollout:** Run manually for 1-2 weeks before setting up Make.com automation

9. **Monitor API usage:** If using Make.com automation, check Anthropic console for API costs

---

## Updating This Workflow

**To add a new client to Deisy's list:**
1. Update "Client Ownership" section above
2. Ensure Monday.com board exists for that client
3. Claude will automatically include in next daily run

**To add a new team member:**
1. Update "Team Structure" section above
2. Update "Task Assignment Logic" if needed for their role
3. Add to appropriate Monday.com boards

**To change automation schedule:**
1. Update "Automation Schedule" section above
2. Update time zone if needed
3. If using Make.com, update the schedule module
4. Inform team of new timing

**To modify client name matching:**
1. Document variations in "Client Ownership" section
2. Example: "Braden (BradenIT, Braden IT)"
3. Claude will match all variations

**To update task assignment rules:**
1. Modify "Task Assignment Logic" table
2. Add examples to "Workflow Example" if helpful
3. Communicate changes to team

---

## Questions or Issues?

Contact Deisy for any questions about this workflow or to suggest improvements to the automation.

---

*Last Updated: February 7, 2026*  
*Version: 2.0*  
*Team: WarmUp*
