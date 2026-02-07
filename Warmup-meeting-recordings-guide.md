Meeting Recording to Monday.com Task Automation Guide - WarmUp Edition
Overview
This guide explains how to automatically process meeting transcripts from Notion and create actionable tasks in Monday.com using Claude with MCP integrations.

Team Structure
Partners & Strategists:

Deisy - Partner & Team Strategist
Mike - Partner & Team Strategist

GTMEs (Go-To-Market Execution):

Paula
Josh
Yasmin

BDR (Business Development Representative):

Mery - Cold calling specialist


Client Ownership
Deisy's Clients:

UBT
Paragon (Paragon Events)
Numina
Braden (BradenIT)
XcelLabs
Crede
VAF
Coya

Mike's Clients:

All other clients (HG Insights, Kelly Schwedland, Sustainment, etc.)


Required Claude Integrations
Before using this workflow, ensure these integrations are enabled in Claude Settings → Integrations:

Notion - To access meeting transcripts
Monday.com - To create and manage tasks


Automation Schedule
Daily at 12:00 PM EST:
Claude automatically:

Searches Notion for new meeting transcripts from the previous day
Identifies client meetings for Deisy's clients only
Extracts WarmUp team action items
Creates tasks in the appropriate Monday.com board
Sets all new tasks to "Review" status


How It Works
1. Meeting Recording

Record client meetings in Notion by pressing the meeting transcription button
Notion will create a transcript page with a title like:

"UBT Onboarding w/ Deisy @Tuesday 9:45 AM"
"Weekly Check In: XcelLabs // WarmUp @Tuesday 12:30 PM"



2. Claude Identifies Client Meetings
Claude searches Notion for meeting transcripts that contain:

✅ Client names from Deisy's client list (matches variations intelligently: "Braden" = "BradenIT", "Paragon" = "Paragon Events")
✅ Meeting titles with these client names

Claude ignores:

❌ Internal WarmUp meetings
❌ Meetings with other clients (Mike's clients)
❌ Meetings without client names in title

3. Task Extraction Rules
What Gets Created:

✅ Action items for WarmUp team members only
✅ Clear, specific deliverables with context
✅ Tasks with identifiable owners

What Gets Ignored:

❌ Client-side action items (e.g., "Client will send brand guidelines")
❌ General discussion points without actions
❌ Tasks that already exist in Monday (checked against last 7 days of Completed tasks)

4. Task Assignment Logic
Claude assigns tasks based on task type and meeting participants:
Task TypeAssigned ToHow Claude DecidesCampaign setup/optimizationGTMEIdentifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned.Email/LinkedIn sequencesGTMEIdentifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned.Technical setup (Clay, Make.com, webhooks)GTMEIdentifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned.Data enrichment/researchGTMEIdentifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned.Reporting/analyticsGTMEIdentifies which GTME was in the meeting from transcript speakers. If multiple GTMEs present, leaves unassigned.Client strategy/planningDeisy or MikeBased on client ownership listCold calling/phone outreachMery (BDR)Always assigned to BDR
GTME Assignment Rules:

✅ If exactly ONE GTME (Paula, Josh, or Yasmin) is in the meeting → Assign GTME tasks to that person
❌ If MULTIPLE GTMEs are in the meeting → Leave GTME tasks unassigned for manual assignment
❌ If NO GTME is in the meeting → Leave GTME tasks unassigned for manual assignment

Strategy Task Assignment:

For Deisy's clients → Assign to Deisy
For all other clients → Assign to Mike

5. Task Properties
Status:

All new tasks automatically set to "Review"

Priority:

Default: Medium
If meeting explicitly mentions "high priority", "urgent", or "critical" → Set to High
Otherwise → Medium

Due Date:

If specific date mentioned in meeting → Use that date
If timeframe mentioned (e.g., "by end of week", "next Tuesday") → Calculate appropriate date
If no due date mentioned → Default to Friday of current week
Remember: Tasks due Friday or earlier = "This Week" group, After Friday = "Upcoming" group

Assignee:

Determined by task type and meeting context (see Task Assignment Logic above)

6. Monday.com Board Structure
Each client has their own board:

Board naming: "[Client Name] Tasks - [GTME Name]"
Examples: "BradenIT Tasks - JOSH", "Coya Tasks - PAULA"

Groups within each board:

This Week - Tasks due by Friday (2 days before end of week)
Upcoming - Tasks due after Friday
Completed - Finished tasks (Claude checks last 7 days for duplicates)

7. Duplicate Prevention
Before creating any task, Claude:

Searches the Monday.com board for similar tasks
Checks "Completed" group for tasks completed in the last 7 days
Compares task descriptions to avoid creating duplicates
Only creates task if it's genuinely new


Manual Task Creation
If you need to process a specific meeting outside the daily automation:
Command for Claude:
Process this Notion meeting transcript for [Client Name]: [Notion link]

Follow the standard meeting recording workflow:
1. Extract WarmUp team tasks only
2. Check for duplicates in Monday
3. Assign based on task type and meeting participants
4. Set priority to Medium unless marked urgent
5. Set due date to end of week if not specified
6. Create in Monday with "Review" status

Workflow Example
Scenario: Tuesday morning meeting with UBT, Josh (GTME) attending

12:30 PM Tuesday: You record the meeting in Notion

Notion creates: "UBT Onboarding w/ Deisy @Tuesday 12:30 PM"


12:00 PM Wednesday (EST): Claude's daily automation runs

Searches Notion for new transcripts
Finds UBT meeting (matches "UBT" from Deisy's client list)
Reviews transcript and extracts:

"Set up Clay table for UBT contact enrichment by end of week" → GTME task
"This is high priority - schedule follow-up strategy call for next week" → Deisy task
"UBT will provide access to their CRM by Friday" → Ignored (client task)




Claude identifies meeting participants:

Deisy present ✓
Josh (GTME) present ✓
Only one GTME, so tasks can be assigned


Claude checks Monday.com "UBT" board:

Searches "Completed" group (last 7 days)
No duplicate tasks found


Claude creates tasks in "UBT" board:

Task 1: "Set up Clay table for UBT contact enrichment"

Group: This Week (due Friday - mentioned "by end of week")
Assignee: Josh (only GTME in meeting)
Priority: Medium (default)
Status: Review


Task 2: "Schedule follow-up strategy call for next week"

Group: Upcoming (due next week)
Assignee: Deisy (client owner)
Priority: High (explicitly mentioned "high priority")
Status: Review




You review tasks:

Check tasks in "Review" status
Adjust due dates, descriptions, or assignments if needed
Change status to move forward




Edge Cases & Special Situations
Multiple GTMEs in meeting:

Example: Both Paula and Josh attend Coya meeting
Result: All GTME tasks left unassigned in Monday
Action: Manually assign tasks after reviewing

Client name variation:

Example: Transcript says "Braden" but client list has "BradenIT"
Result: Claude intelligently matches and processes normally
Matches: "Paragon" = "Paragon Events", "Braden" = "BradenIT", "XCel" = "XcelLabs"

Ambiguous due dates:

Example: "Get this done soon" or "ASAP"
Result: Defaults to Friday of current week
Action: Review and adjust manually if needed

Mixed priority signals:

Example: "Important but not urgent"
Result: Defaults to Medium unless "high priority", "urgent", or "critical" explicitly stated
Action: Adjust priority in Monday if needed

No clear task owner:

Example: "Someone needs to check on this"
Result: Claude will attempt to assign based on task type, may leave unassigned if unclear
Action: Manually assign during review


Troubleshooting
Meeting transcript not found:

Verify client name is in the Notion page title
Check that recording was completed (not just started)
Ensure meeting happened within last 24 hours
Try manual processing with direct Notion link

Wrong person assigned:

Check if correct GTME was identified in transcript speakers
For strategy tasks, verify client is in correct ownership list
Manually reassign in Monday if needed

Duplicate tasks created:

May indicate task name/description varies significantly
Check if previous task was in "Completed" group older than 7 days
Mark as duplicate and delete in Monday

Task in wrong group:

Verify due date interpretation from meeting notes
Remember: Friday or before = "This Week", After Friday = "Upcoming"
Manually move between groups as needed

No tasks created from meeting:

All action items may have been client-side
Meeting may have been informational only
Check Notion transcript exists and is complete
Verify client name matches Deisy's client list (with variations)

Wrong priority assigned:

Claude looks for explicit mentions of "high priority", "urgent", "critical"
Other urgency language may not trigger High priority
Manually adjust in Monday after review

Multiple GTMEs, but tasks assigned anyway:

Report to Deisy - may indicate speaker identification issue
Manually verify and reassign if needed


Best Practices

Clear action items in meetings: State clearly "WarmUp will [do X]" vs "Client will [do Y]"
Mention names: Reference team members by name in meetings to help Claude assign correctly
Due dates: Mention specific timeframes in meetings ("by end of week", "by next Tuesday", "by Friday")
Priority: Explicitly say "this is high priority" or "this is urgent" for important tasks
Review daily: Check "Review" status tasks in Monday.com each afternoon after the 12pm EST automation runs
Single GTME meetings: When possible, have one GTME per client meeting to enable automatic assignment
Provide feedback: If Claude consistently misassigns or misinterprets, update this guide


Updating This Workflow
To add a new client to Deisy's list:

Update "Client Ownership" section above
Ensure Monday.com board exists for that client
Claude will automatically include in next daily run

To add a new team member:

Update "Team Structure" section above
Update "Task Assignment Logic" if needed for their role
Add to appropriate Monday.com boards

To change automation schedule:

Update "Automation Schedule" section above
Update time zone if needed
Inform team of new timing

To modify client name matching:

Document variations in "Client Ownership" section
Example: "Braden (BradenIT, Braden IT)"
Claude will match all variations


Questions or Issues?
Contact Deisy for any questions about this workflow or to suggest improvements to the automation.

Last Updated: February 7, 2026
Version: 1.0
Team: WarmUp
