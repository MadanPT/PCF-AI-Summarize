# PCF-AI-Summarize
________________________________________
AI Call Summary Generation – Azure Functions + AI Foundry + PCF + Dynamics 365
 Overview
This solution enables automatic call summary generation inside Dynamics 365 CRM Activities using Azure AI Foundry Agents.
Users enter call notes in a custom PCF control, click a button, and instantly receive an AI-generated call summary, powered by GPT-5 Chat, through an Azure Function API.
________________________________________
# High-Level Architecture

 <img width="800" height="800" alt="Image" src="https://github.com/user-attachments/assets/ec1c4e49-6f4a-4d33-8df1-c97f07406b1f" />

# Flow
Dynamics 365 (Activity Form)
        |
        |  (PCF Control API Call)
        v
Azure Function (HTTP Trigger)
        |
        |  (Agent Client + Thread + Message)
        v
Azure AI Foundry (GPT-5 Chat Agent)
        |
        |  (Streaming AI Response)
        v
Azure Function
        |
        |  (HTTP Response)
        v
PCF Control (Read-only Summary Textbox)


 
________________________________________
# Key Components
1. Azure Functions
•	HTTP-triggered Azure Function
•	Acts as a backend API for the PCF control
•	Deployed to Azure Cloud
2. Azure AI Foundry
•	Uses Persistent AI Agent Client
•	Model used: gpt-5-chat
•	Handles long-running conversations using threads
3. PCF Control (PowerApps Component Framework)
•	Hosted inside Dynamics 365 CRM Activities
•	UI Elements:
o	Input Textbox – Editable (Call Notes)
o	Button – Generate Summary
o	Output Textbox – Read-only (AI Summary)
________________________________________
# End-to-End Flow
Step-by-Step Execution
1.	User enters Call Notes
o	Inside Dynamics 365 Activity form
o	Using custom PCF control
2.	User clicks “Generate Summary”
o	PCF control sends HTTP request to Azure Function
3.	Azure Function is triggered
o	Receives call notes as input payload
4.	Persistent Agent Client is created
o	Uses Azure AI Foundry endpoint
o	Ensures agent continuity and scalability
5.	AI Agent is created
o	Model: gpt-5-chat
o	Configured for conversational summarization
6.	New Thread is created
o	Represents a single summarization context
7.	Chat Message is created
o	User input (call notes) passed as message content
8.	RunStreamingAsync is executed
o	Message sent to AI Agent
o	AI processes notes and generates summary
o	Streaming response allows efficient handling
9.	AI Response is received
o	Final output: Call Summary
10.	Azure Function returns HTTP response
o	Summary returned as API response
11.	PCF Control displays summary
o	Read-only textbox shows AI-generated result
________________________________________
# AI Capabilities
•	Summarizes long and unstructured call notes
•	Extracts:
o	Key discussion points
o	Action items
o	Follow-ups
•	Ensures consistent call documentation inside CRM
________________________________________
# Deployment Details
Azure Function
•	Deployed to Azure App Service
•	Secured using Azure Identity / Managed Identity
•	Scalable and stateless
PCF Control
•	Packaged and deployed via Power Platform
•	Bound to Dynamics 365 Activity forms
________________________________________
# Security & Best Practices
•	No AI keys exposed to client (PCF)
•	All AI calls handled server-side
•	Supports future enhancements:
o	Authentication
o	Logging & monitoring
o	Rate limiting
________________________________________
# Benefits
•	⏱️ Saves user time on manual call summaries
•	📄 Improves CRM data quality
•	🤖 Leverages latest Azure AI models
•	🔌 Clean separation of UI (PCF) and AI logic (Azure Functions)
•	📈 Scalable and cloud-native design
________________________________________
# Future Enhancements (Optional)
•	Multi-language call summaries
•	Sentiment analysis
•	Action item extraction
•	Storing summaries directly in CRM fields
•	Support for voice-to-text integration
________________________________________
# Tech Stack
•	Azure Functions
•	Azure AI Foundry
•	GPT-5 Chat Model
•	C# (.NET)
•	PCF (TypeScript)
•	Dynamics 365 / Dataverse
________________________________________
# Conclusion
This solution seamlessly integrates AI-powered summarization into Dynamics 365, providing a modern, scalable, and secure approach to enhance CRM productivity using Azure AI Foundry Agents.
________________________________________

 
