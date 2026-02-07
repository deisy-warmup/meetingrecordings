Meeting Recording to Task Management Automation Guide - Generic Template
Overview
This guide explains how to automatically process meeting transcripts and create actionable tasks in your project management tool using Claude with AI integrations.
Customize this template for your team by replacing bracketed placeholders [like this] with your specific information.

Software Requirements
Required Tools
AI Assistant:

Claude (by Anthropic)

Free or paid account at claude.ai
Required integrations: see setup section below



Meeting Transcription (Choose ONE):

Notion - AI-powered meeting notes and transcriptions
Google Docs - Manual or automated transcription via Google Meet
Microsoft Word/OneNote - Manual or automated transcription via Teams
Otter.ai - Automated meeting transcription
Other: Any tool that creates searchable text transcripts

Task Management (Choose ONE):

Monday.com - Visual project management
Jira - Agile project management (Software/Work Management)
Asana - Team task management
ClickUp - All-in-one project management
Other: Any tool with Claude integration or API access


First-Time Setup: Define Your Team
Before using this workflow, you need to tell Claude about your team structure. On your first run, Claude will ask you these questions:
Team Structure Questions
1. What roles exist on your team?
Common roles that use Claude:

Project Managers - Oversee projects, coordinate teams, track deliverables
Product Managers - Define product strategy, prioritize features, manage roadmaps
Engineers/Developers - Build software, fix bugs, implement features
Designers - Create UI/UX, graphics, user flows
Content Writers - Write articles, documentation, marketing copy
Marketing Specialists - Run campaigns, create content, analyze metrics
Sales Representatives - Handle deals, client relationships, outreach
Account Managers - Manage client relationships and projects
Data Analysts - Analyze data, create reports, provide insights
Executives/Leadership - Strategy, decision-making, oversight
Operations Specialists - Process optimization, workflow management
Customer Success - Client support, onboarding, retention

Or define your own custom roles
2. Who is on your team and what do they do?
Example format:

[Name] - [Role] - [Responsibilities]
Jane Doe - Product Manager - Defines features, prioritizes roadmap, stakeholder communication
John Smith - Senior Developer - Technical implementation, code reviews, architecture decisions

3. Who owns which clients/projects?
Example:

Jane Doe's Projects: Project Alpha, Project Beta
John Smith's Projects: Project Gamma

4. What types of tasks does each role handle?
Example:

Product Managers: Strategy, roadmap planning, requirements documentation
Developers: Feature implementation, bug fixes, technical documentation
Designers: UI mockups, user research, design systems


Required Claude Integrations
Step 1: Connect Meeting Transcription Tool
If using Notion:

Go to Claude.ai → Settings → Integrations
Find Notion and click Connect
Authorize Claude to access your Notion workspace
Grant access to workspace containing meeting notes

If using Google Docs:

Claude doesn't have direct Google Docs integration yet
Alternative: Copy/paste meeting transcript into Claude
Or use Google Drive API with custom setup (advanced)

If using other tools:

Check if Claude has a native integration in Settings → Integrations
If not available, you'll need to copy/paste transcripts manually

Step 2: Connect Task Management Tool
If using Monday.com:

In Claude Settings → Integrations
Find Monday.com and click Connect
Authorize Claude to access your Monday.com account

If using Jira:

Claude doesn't have native Jira integration currently
Alternative: Use Jira's API with Claude Code or custom automation
Or copy Claude's task suggestions and manually create in Jira

If using other tools:

Check Claude Settings → Integrations for your tool
If not available, consider API-based automation or manual entry

Step 3: Connect GitHub (Optional)
If you want Claude to remember this guide:

Store this guide in a GitHub repository
Claude can fetch it each time using the repository URL
No GitHub integration needed - public repositories work directly


How to Execute the Workflow
First-Time Run
On your very first run, use this command:
I'm setting up the meeting recordings workflow. Please ask me about my team structure:
1. What roles exist on my team
2. Who is on the team and what they do
3. Who owns which clients/projects
4. What types of tasks each role handles

After I answer, save this information and help me set up the workflow.
Claude will ask you questions and save your team structure for future use.

Daily Command
Once setup is complete, use this command each workday:
If storing guide in GitHub:
Read my meeting workflow guide from [Your GitHub URL]
Then process this week's meeting transcripts following the guide.
If not using GitHub:
Process this week's meeting transcripts:
- Search [Notion/Google Docs/Tool] for meeting notes from Monday through today
- Identify client/project meetings for [Your Team]
- Extract action items for our team only (not client tasks)
- Check [Monday/Jira/Tool] for duplicate tasks
- Create new tasks with appropriate status
- Assign based on task type and team structure
- Mark transcripts as processed

Workflow Rules
1. Time Window

Process meetings from: Current week (Monday through today)
Ignore: Previous weeks' meetings
Reset: Each Monday, new week begins

2. Duplicate Prevention
Method 1: Mark Processed (Recommended for Notion)

After processing, mark meeting page with "Processed" checkbox
Skip any meetings already marked "Processed"
Prevents reprocessing same meeting multiple times

Method 2: Check Recent Tasks (For all tools)

Before creating task, search task management tool
Check last 7 days of completed tasks
Only create if genuinely new

3. Meeting Identification
Identify as client/project meeting if:

✅ Title contains client/project name
✅ Has external attendees (not just internal team)
✅ Creates action items for your team

Skip if:

❌ Internal team meeting only
❌ Informational/no action items
❌ Different team/department meeting

4. Task Extraction Rules
Create tasks for:

✅ Action items for YOUR team members
✅ Clear, specific deliverables
✅ Items with identifiable owners
✅ Follow-ups, deadlines, commitments

Ignore:

❌ Client/external party action items
❌ General discussion points without actions
❌ FYI information
❌ Decisions already documented

5. Task Assignment Logic
Create a table like this for your team:
Task TypeAssigned ToDecision Rule[e.g., Feature development][Role: Engineer][Look for: technical implementation, coding, architecture][e.g., Design work][Role: Designer][Look for: UI, UX, mockups, visual design][e.g., Content creation][Role: Writer][Look for: blog posts, documentation, copy][e.g., Strategy/planning][Role: PM/Manager][Look for: roadmap, prioritization, stakeholder management][e.g., Client communication][Role: Account Manager][Look for: client updates, relationship management]
Assignment Priority:

Check if specific person mentioned in meeting ("John will handle this")
Match task type to role responsibilities
Consider who attended the meeting
If unclear, leave unassigned for manual review

6. Task Properties
Status:

New tasks → "To Review" or "Backlog" (customize for your workflow)
Allows manual review before moving to active status

Priority:

Default: Medium
High if meeting mentions: "urgent", "high priority", "critical", "ASAP"
Low if mentions: "nice to have", "future", "low priority"

Due Date:

If specific date mentioned → Use that date
If "end of week" → Friday of current week
If "next week" → Friday of next week
If "end of month" → Last day of current month
No date mentioned → Default to end of current week

Labels/Tags (Optional):

Add client/project name
Add meeting date
Add "from-meeting" tag for tracking


Task Management Tool Specifics
For Monday.com Users
Board Structure:

One board per client/project recommended
Groups: "This Week", "Upcoming", "Completed"
Custom statuses: adapt to your workflow

Creating Tasks:

Claude can create items directly via Monday.com integration
Sets: name, status, assignee, due date, priority, description
Groups items by due date automatically

For Jira Users
Project Structure:

One project per client/product
Issue types: Story, Task, Bug (adapt to your setup)
Sprints/Backlog organization

Creating Tasks:

Claude generates task details
You create issues manually or via automation
Include: Summary, Description, Assignee, Due Date, Priority, Labels

Alternative - Jira Automation:

Use Jira's built-in automation rules
Trigger: Email or webhook from Claude
Action: Create issue with details

For Other Tools
Asana:

Check if Claude integration available (Settings → Integrations)
Structure: Projects → Sections → Tasks
Similar workflow to Monday.com

ClickUp:

Check integration availability
Structure: Spaces → Folders → Lists → Tasks
Rich task properties similar to Monday.com

Generic Approach:

Claude extracts tasks into structured format
You copy/paste into your tool
Or use tool's API with custom automation


Example Workflow
Scenario: Wednesday afternoon, want to process this week's meetings
You run:
Process this week's meeting transcripts
Claude does:

Searches meeting notes (Notion/Google Docs/etc.)

Finds: "Client ABC Kickoff - Monday 10am"
Finds: "Project XYZ Status - Tuesday 2pm"
Finds: "Internal Team Sync - Wednesday 9am" (skips - internal only)


Reviews "Client ABC Kickoff" transcript

Extracts: "We need to send over the project timeline by Friday"
Extracts: "Design mockups due next Tuesday"
Extracts: "Client will provide access credentials" (skips - client action)


Checks for duplicates

Searches Monday/Jira for existing "project timeline" tasks
None found → OK to create


Creates tasks:

Task 1: "Send project timeline to Client ABC"

Assigned to: Project Manager (client communication)
Due: Friday (mentioned in meeting)
Priority: Medium
Status: To Review


Task 2: "Create design mockups for Client ABC"

Assigned to: Designer (design work)
Due: Next Tuesday
Priority: Medium
Status: To Review




Marks meetings as processed

Adds "Processed" checkbox to both meeting pages
Won't reprocess on next run


Reports back:

"Created 2 tasks from 2 meetings"
"Skipped 1 internal meeting"
"Marked 2 meetings as processed"




Troubleshooting
Claude can't find meetings:

Verify meeting notes are in searchable format (text, not images)
Check date range (current week only)
Confirm client/project names in meeting titles
Try searching manually to verify notes exist

Wrong person assigned:

Review task assignment rules in this guide
Update rules to better match your team structure
Manually reassign in task management tool
Provide feedback to improve future assignments

Duplicate tasks created:

Check if "Processed" marking is working
Verify duplicate check looks back far enough (7 days default)
May need to adjust duplicate detection logic
Manually delete duplicates and mark meeting as processed

Can't connect integration:

Verify tool has Claude integration available
Check you have proper permissions in the tool
Try disconnecting and reconnecting
Consider alternative approaches (API, manual)

Tasks missing important details:

Meeting notes may lack specific information
Train team to document action items clearly in meetings
Include: Who, What, When in meeting notes
Review and enhance tasks manually as needed

Integration isn't available for my tool:

Check Claude's integrations list (new ones added regularly)
Use API-based automation if tool has API
Manual approach: Claude extracts, you create tasks
Consider switching to supported tool if automation is priority


Best Practices

Clear action items in meetings

State explicitly: "We will [do X]" vs "They will [do Y]"
Mention names: "Sarah will handle the design"
Specify timeframes: "by Friday", "next week", "before the deadline"


Consistent meeting note structure

Use templates for meeting notes
Clear sections: Attendees, Discussion, Action Items
Tag client/project names in titles


Run regularly

Daily or every other day works best
Don't let meetings pile up
Easier to process fresh notes with context


Review before finalizing

Tasks created with "Review" status
Check assignments, due dates, priorities
Add context or details as needed
Then move to active status


Provide feedback

If Claude consistently misassigns or misses items
Update this guide with clearer rules
Refine task type → role mappings
Improve meeting note templates


Keep team structure updated

When team members join/leave
When roles or responsibilities change
When new clients/projects start
Update this guide and inform Claude




Customization Guide
Adding a New Team Member

Update team structure section with:

Name, Role, Responsibilities
Client/project ownership
Task types they handle


Update task assignment table with their role
Inform Claude: "Update team structure: [name] joined as [role] handling [responsibilities]"

Adding a New Client/Project

Update client/project ownership section
Ensure task management board/project exists
Inform Claude: "[Name] is now managing [Client/Project]"

Changing Task Assignment Rules

Update task assignment logic table
Add examples if helpful
Test with a few meetings
Refine based on results

Switching Tools
If changing meeting transcription tool:

Update "Software Requirements" section
Update "Connect Meeting Transcription Tool" steps
Update daily command with new tool name
Test with sample meeting

If changing task management tool:

Update "Software Requirements" section
Update integration connection steps
Update task management tool specifics section
Adjust task properties to match new tool
Test with sample tasks


Advanced: Full Automation
For hands-off automation using APIs and scheduling tools:
Prerequisites

API access for your meeting and task management tools
Scheduling/automation platform (Zapier, Make.com, n8n)
Anthropic API key for Claude access

High-Level Setup

Schedule trigger (daily at chosen time)
Call Claude API with workflow instructions
Claude processes meetings and generates task list
Create tasks via task management tool API
Send notification (optional - Slack, email)

Considerations

API costs for Claude and other services
Error handling and monitoring
Testing and validation period
Maintenance and updates

Detailed automation setup varies by tools - consult each tool's API documentation

Support & Maintenance
Updating This Guide:

Keep team structure current
Refine rules based on experience
Document special cases and edge cases
Version control if using GitHub

Getting Help:

Check Claude's documentation: docs.anthropic.com
Tool-specific help: Each tool's support documentation
Community: Share learnings with your team

Providing Feedback:

If workflow isn't working well, revisit rules
Gather team feedback on assignments and task quality
Iterate and improve over time


FAQ
Q: Do all team members need Claude accounts?
A: Only those who will run the workflow. Others just use the created tasks.
Q: How much does this cost?
A: Claude has free and paid tiers. Check claude.ai/pricing. Task management tools have separate pricing.
Q: Can I use multiple meeting transcription tools?
A: Yes, but you'll need to specify which tool to search each time, or set a primary tool.
Q: What if my tool isn't supported?
A: You can still use Claude to extract tasks and manually create them, or explore API automation.
Q: How long does processing take?
A: 2-5 minutes typically, depending on number of meetings and tool response times.
Q: Can I process meetings from last week?
A: Yes, adjust the time window in your command. Default is current week only to prevent reprocessing.
Q: What if I don't want automation?
A: You can run this manually whenever needed. Just paste the command when you want to process meetings.

Template Version: 1.0
Last Updated: February 2026
License: Feel free to adapt for your team

Ready to use this guide?

Copy this template
Fill in your team information
Set up required integrations
Run the first-time setup with Claude
Start processing meetings!
