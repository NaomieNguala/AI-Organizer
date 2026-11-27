Email Classifier Model Workflow
The following readme documents the model's implementation and workflow, from receiving an email to categorizing it and sending notifications.
A.1. Outlook Categories
Five categories were created in Outlook, each with a distinct color for easier identification and organization of incoming emails:
•	School
•	Work
•	Financial
•	Advertisement
•	General
A.2. Email Trigger and Text Processing
Power Automate was configured with the When a new email arrives (V3) trigger to monitor incoming emails in the Inbox.
An HTML to text action was added to convert the email body into readable text before sending it to AI Builder for analysis.
A.3. AI Builder Email Analysis
A custom AI Builder prompt named Email Analyzer was created with two inputs:
•	Email Subject
•	Email Body
The prompt analyzes the email and returns the following information:
Output	Purpose
Category	Assigns one of the five email categories.
Priority	Determines whether the email is High, Medium, or Low priority.
Action Required	Identifies whether the email requires the user's attention or a response.
Deadline	Extracts a deadline when one is mentioned.
Summary	Provides a concise summary of the email.
Reason	Explains why the email was assigned its priority level.
A.4. Email Categorization
Power Automate uses the AI Builder results to assign the appropriate Outlook category to the incoming email. This allows emails to be organized automatically without requiring manual sorting.
A.5. Notification System
The notification system is based on the priority level assigned by AI Builder.
•	High Priority: Emails with deadlines within 48 hours are classified as High priority.
•	Medium Priority: Emails with deadlines beyond 48 hours or no clearly stated deadlines are classified as Medium priority.
•	Low Priority: Informational emails that do not require immediate attention are classified as Low priority and do not trigger notifications.
Notification messages contain the original email's subject, priority level, category, and summary. Depending on the priority level, the flow sends a notification to alert the recipient of emails requiring attention.
A.6. Trigger Loop Prevention
To prevent the flow from processing its own notification emails, advanced trigger conditions were modified to exclude automatically generated notifications. This prevents notifications from triggering the workflow again and generating duplicate messages or an infinite loop.
A.7. Testing and Evaluation
The model was tested using emails representing all five categories. Microsoft Excel was used to record the test data and evaluate the categorization results and notification behavior.
