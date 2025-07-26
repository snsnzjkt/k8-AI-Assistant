# k8: AI Personal Assistant

A comprehensive AI-powered personal assistant built with n8n that helps you manage emails, calendar events, and contacts through natural language commands via Telegram.

## Overview

This project consists of a modular AI assistant system that can handle various personal productivity tasks through specialized agents. The system is triggered via Telegram messages and uses AI to route requests to the appropriate specialized workflows.

## Architecture

The system follows a modular architecture with the following components:

### Main Workflow
- **Entry Point**: Telegram bot integration
- **AI Router**: Main assistant agent that routes queries to specialized sub-agents
- **Memory**: Conversation memory to maintain context across interactions
- **Response Handler**: Sends responses back to Telegram

### Specialized Agents

#### 1. Email Agent
Handles all email-related operations:
- **Send emails** with HTML formatting
- **Create drafts** for later editing
- **Retrieve emails** with filtering options
- **Reply to emails** with context
- **Label/flag emails** for organization
- **Mark emails as unread**

#### 2. Calendar Agent
Manages calendar events and scheduling:
- **Create events** (solo or with attendees)
- **Get calendar schedules** for specific date ranges
- **Update existing events** (time, details)
- **Delete events** when no longer needed

#### 3. Contact Agent
Manages contact information:
- **Search contacts** by name or details
- **Add new contacts** with name, email, and phone
- **Update existing contact** information

## Features

### 🤖 Natural Language Processing
- Understands conversational requests
- Routes queries to appropriate specialized agents
- Maintains conversation context and memory

### 📧 Email Management
- Professional HTML email formatting
- Automatic signature as "Kate"
- Email retrieval with sender filtering
- Label management and organization
- Reply functionality with threading

### 📅 Calendar Integration
- Google Calendar synchronization
- Event creation with attendee management
- Flexible scheduling with automatic 1-hour default duration
- Event modification and deletion

### 👥 Contact Management
- Airtable-based contact storage
- Search and retrieval capabilities
- Add/update contact information
- Integration with email and calendar for attendee lookup

### 💬 Telegram Interface
- Real-time messaging interface
- Session-based memory per user
- Error handling with retry mechanisms

## Technical Stack

- **Workflow Engine**: n8n
- **AI Models**: 
  - OpenAI GPT-4o (for specialized agents)
  - DeepSeek Chat v3 (for main routing agent)
- **Messaging**: Telegram Bot API
- **Email**: Gmail API integration
- **Calendar**: Google Calendar API
- **Contact Storage**: Airtable API
- **Memory**: Buffer window memory with session management

## Setup Requirements

### Prerequisites
1. n8n instance (self-hosted or cloud)
2. API credentials for:
   - OpenAI or OpenRouter
   - Gmail (OAuth2)
   - Google Calendar (OAuth2)
   - Airtable (Personal Access Token)
   - Telegram Bot API

### Installation Steps

1. **Import Workflows**
   - Import all four JSON workflow files into your n8n instance
   - Main Workflow.json (entry point)
   - Email Agent.json
   - Calendar Agent.json
   - Contact Agent.json

2. **Configure Credentials**
   - Set up Gmail OAuth2 for email operations
   - Configure Google Calendar OAuth2 for calendar access
   - Add Airtable Personal Access Token for contact management
   - Create Telegram bot and add API credentials
   - Add OpenAI/OpenRouter API keys

3. **Setup Airtable**
   - Create a "Contacts" base in Airtable
   - Add fields: name, email, phoneNumber
   - Update the base and table IDs in the Contact Agent workflow

4. **Configure Calendar**
   - Update the calendar email address in Calendar Agent nodes
   - Ensure proper permissions for calendar access

5. **Activate Workflows**
   - Start with activating the Main Workflow
   - The sub-workflows (agents) are called automatically

## Usage Examples

### Email Operations
```
"Send an email to John asking about the meeting time"
"Create a draft email to the team about project updates"
"Show me emails from Sarah from last week"
"Reply to the latest email from Mike"
```

### Calendar Management
```
"Schedule a meeting with Alice tomorrow at 2 PM"
"What's on my calendar for today?"
"Move my 3 PM meeting to 4 PM"
"Cancel the team standup on Friday"
```

### Contact Management
```
"Add John Smith's contact: john@example.com, 555-1234"
"Find Alice's email address"
"Update Mike's phone number to 555-9876"
```

## System Flow

1. **User sends message** to Telegram bot
2. **Main Agent receives** and analyzes the request
3. **Routing decision** made based on request type
4. **Contact lookup** performed if needed (for emails/calendar invites)
5. **Specialized agent** executes the specific task
6. **Think tool** verifies the action was completed correctly
7. **Response sent** back to user via Telegram

## Error Handling

- Each agent has error handling with "Try Again" fallback responses
- Memory system maintains context even after errors
- Validation steps ensure required information is gathered before actions

## Customization

### Adding New Capabilities
1. Create new specialized agent workflow
2. Add as a tool in the Main Workflow
3. Update the system message with new tool description
4. Define when to route requests to the new agent

### Modifying Responses
- Update system messages in each agent
- Customize email signatures and formatting
- Adjust error messages and fallback responses

## Security Considerations

- All API credentials are stored securely in n8n
- OAuth2 used for Google services (Gmail, Calendar)
- Session-based memory isolates conversations
- No sensitive data stored in workflow configurations

## Limitations

- Requires active internet connection for all operations
- Dependent on third-party API availability
- Email operations limited to connected Gmail account
- Calendar operations limited to connected Google Calendar
- Contact storage limited to configured Airtable base

## Support

For issues or questions:
1. Check n8n logs for error details
2. Verify API credentials are properly configured
3. Ensure all required permissions are granted
4. Test individual agents separately for debugging

## License

This project is designed for personal use. Ensure compliance with all third-party service terms of use.
