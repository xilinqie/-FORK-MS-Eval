You are a support operations analyst. Analyze the support center performance using the support tickets database.

Calculate SLA compliance and customer satisfaction metrics per ticket priority. For SLA compliance, use these response time thresholds: High priority tickets must be responded to within 4 hours, Medium within 8 hours, and Low within 24 hours.

For each priority level compute the total ticket count, the number of SLA-compliant tickets, the compliance rate as a percentage rounded to 2 decimal places, and the average customer satisfaction score rounded to 2 decimal places.

All numeric values (ticket counts, compliance rates, CSAT scores) must be written as plain numbers without percent signs, currency symbols, thousand separators, or spreadsheet formulas. For example, write the compliance rate as 12.03 (meaning 12.03%), not as "12.03%", "12.03 %", "12", or "=COUNT(...)/...".

Create a Google Sheet titled Support Center Performance Dashboard with two sheets:

Sheet named SLA_Compliance with columns: Priority, Total_Tickets, SLA_Compliant, Compliance_Rate, Avg_CSAT. Include one row per priority (High, Medium, Low).

Sheet named Summary with two columns: Metric and Value. Include: Best_Priority (priority with highest average CSAT score) and Worst_SLA_Priority (priority with lowest SLA compliance rate).

Create a Google Forms survey titled Customer Support Satisfaction Survey with exactly 4 questions. The first question asks whether the issue was resolved satisfactorily with Yes, No, and Partially as options. The second asks how the customer would rate the response speed with numeric options from 1 to 5. The third asks how they would rate the support agent with numeric options from 1 to 5. The fourth asks whether they would contact the support team again with Yes and No as options.

Send an email from analytics@company.example.com to support-management@company.example.com with subject Support Center Performance Report - SLA Compliance Analysis. The body should summarize key findings including SLA compliance rates and CSAT scores.

The SLA_Policy_Reference.pdf file in your workspace contains the SLA policy documentation for reference.

Task-Solving Rationable with Sub-task Decomposition:
To solve this task efficiently, keep the compact read-only analysis in the main agent, then dispatch one parallel writer wave with two external-workflow-operator Coder sub-agents, one per independent resource. Resolve the workspace, extract `SLA_Policy_Reference.pdf` with authorized local Python, inspect the support-ticket schema, and run one set-based aggregate for exactly High, Medium, and Low using response-time thresholds 4, 8, and 24 hours. Freeze numeric Total_Tickets, SLA_Compliant, 0–100 Compliance_Rate, Avg_CSAT, and raw denominators; rank Best_Priority by rounded two-decimal Avg_CSAT with deterministic ties and Worst_SLA_Priority by raw compliance rate.

Wave 1 — after the main agent has frozen the aggregate, dispatch exactly two Coder sub-agents concurrently in the same response. Pass each its literal resource title and write contract; pass the numeric aggregate and summary rankings to the Sheet owner. The two owners write different external resources and do not wait for each other.

1. coder 0 (external-workflow-operator 0): Sole owner of the `Support Center Performance Dashboard` Google spreadsheet. Search/reuse one exact-title spreadsheet or create once on zero matches; block duplicate titles/tabs, maintain only `SLA_Compliance` and `Summary`, and write the exact `Priority, Total_Tickets, SLA_Compliant, Compliance_Rate, Avg_CSAT` headers with exactly High, Medium, Low rows. Counts, rates, and CSAT are plain numeric cells; write rates on the 0–100 scale and rates/CSAT rounded to two decimals, without percent signs, currency symbols, thousands separators, or formulas. `Summary` has `Metric, Value` and the `Best_Priority` and `Worst_SLA_Priority` rows from the frozen aggregate. Read both bounded populated ranges back and return spreadsheet ID, sheet identities, row counts, and exact cell comparisons. Do not create the form or send email.
2. coder 1 (external-workflow-operator 1): Sole owner of the `Customer Support Satisfaction Survey` form. Call `create_form` exactly once, retain `formId`, and add exactly four task-worded questions sequentially: satisfactory issue resolution with `Yes/No/Partially`; response speed with `1/2/3/4/5`; support agent rating with `1/2/3/4/5`; and whether the customer would contact support again with `Yes/No`. Call `get_form` and verify title, four-question order, wording, types, and option sets; never retry an ambiguous create. Return the actual form ID and read-back controls. Do not write the spreadsheet or send email.

While the two writers run, the main agent independently exhausts Sent pages for exact recipient `support-management@company.example.com` and subject `Support Center Performance Report - SLA Compliance Analysis`. Send the missing message at most once with the supported `send_email` parameter `from_addr="analytics@company.example.com"`, the exact recipient and subject, and all three SLA rates and CSAT values plus the key findings. If the tool rejects that sender, report the concrete failure rather than silently changing it. Read the retained message and verify its From, To, subject and body. The email summarizes the frozen analysis and does not assert that either still-running resource is complete, so it need not wait for those writers. Final completion waits for both writer read-backs and the retained email; reconcile Sheet, Form, and email directly to the frozen aggregate and finish without an auditor. Only the main agent declares completion.
