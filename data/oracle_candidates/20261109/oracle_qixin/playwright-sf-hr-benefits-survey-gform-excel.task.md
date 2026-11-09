You are an HR benefits administrator at a large company. The company is evaluating whether its benefits package is competitive compared to industry peers. A market research firm has published a benefits comparison report on a website at http://localhost:30212/benefits_comparison.html showing competitor companies' benefits packages including health insurance coverage percentages, annual PTO days, and retirement matching percentages.

Read the Benefits_Review_Guide.pdf in your workspace to understand the evaluation framework and reporting requirements.

First, browse the competitor benefits comparison website and extract the benefits data for all listed competitor companies. Then query the employee database to retrieve department-level satisfaction metrics. Specifically, get the average job satisfaction score and the average work-life balance score for each department, along with the department headcount.

Create a Google Form titled "Employee Benefits Improvement Survey" with the following questions. Question 1: "Which department are you in?" as a single-select multiple choice question with all seven department names as choices. Question 2: "How satisfied are you with current health insurance coverage? (1-5)" as a multiple choice question with answer options 1, 2, 3, 4, and 5. Question 3: "How satisfied are you with current PTO policy? (1-5)" as a multiple choice question with answer options 1, 2, 3, 4, and 5. Question 4: "How satisfied are you with retirement matching? (1-5)" as a multiple choice question with answer options 1, 2, 3, 4, and 5. Question 5: "Which benefit improvement would you prioritize?" as a multiple choice question with options "Better Health Insurance", "More PTO Days", "Higher Retirement Match", and "Other". All questions should be required.

Create an Excel workbook called Benefits_Analysis.xlsx in your workspace with three sheets. Write all numeric values directly as literal numbers (for example 90 or 4.5); do not use Excel formulas.

The first sheet should be called "Competitor Comparison" with columns: Company, Health_Insurance_Pct, PTO_Days, Retirement_Match_Pct. Include all competitor companies from the website plus a row for "Our Company" with values of 80 percent health insurance, 20 PTO days, and 4.0 percent retirement match. Sort all rows alphabetically by Company.

The second sheet should be called "Department Satisfaction" with columns: Department, Avg_Job_Satisfaction, Avg_Work_Life_Balance, Headcount, Satisfaction_Rating. The satisfaction data should come from the employee database. Round each department's average job satisfaction and average work-life balance to two decimal places. The Satisfaction_Rating column should be "High" if the average job satisfaction (rounded to two decimal places) is 6.55 or above, and "Moderate" otherwise. Sort by Department alphabetically.

The third sheet should be called "Gap Analysis" with columns: Benefit_Category, Our_Value, Market_Average, Gap, Priority. For each of the three benefit categories (Health Insurance, PTO Days, Retirement Match), compute the market average from competitor data (rounded to 1 decimal), calculate the gap as our value minus the market average (rounded to 1 decimal), and set Priority to "High" if the gap is negative, "Medium" if the gap is zero or slightly positive (within 1.0), and "Low" if the gap is more than 1.0 above market average.

Send an email to hr_leadership@company.com with the subject "Benefits Competitiveness Analysis & Survey Launch". The body should summarize the key gaps found and mention that the employee survey has been created for additional input.

When you are finished, call claim_done.

Task-Solving Rationable with Sub-task Decomposition:
To solve this task efficiently, the main agent executes the whole task directly with no sub-agent delegation. Resolve the task-visible agent-workspace absolute path from the Visible Boundary or allowed workspace listing and read <agent_workspace>/Benefits_Review_Guide.pdf for the evaluation framework and reporting requirements. Preserve the task's exact filenames, question types, choices, and required flags when applying that guidance.

Start the independent web and warehouse reads in native parallel. The web branch extracts the competitor benefits data: use only browser_navigate on http://localhost:30212/benefits_comparison.html followed by one browser_snapshot. Within the web branch, do not call browser_install, terminal, PDF, Snowflake, email, or artifact tools, and do not retry alternate URLs or tool names. This branch-local tool restriction does not prevent the separate warehouse query from running concurrently. Capture every visible competitor row as {company, health_insurance_pct, pto_days, retirement_match_pct}. If navigation or the snapshot fails, stop on the exact blocker instead of guessing values.

In the independent warehouse branch, query the employee database; it does not consume competitor rows. Identify the task-visible employee table and department, job-satisfaction, and work-life-balance fields through the granted schema tools when needed, then run one set-based Snowflake query for all seven departments' headcount, raw average job satisfaction, and raw average work-life balance. Do not export individual employee records. Require seven distinct department names and complete source rows; missing or ambiguous source data is a blocker.

The main agent freezes one literal canonical payload. Include every competitor plus Our Company with Health_Insurance_Pct=80, PTO_Days=20, and Retirement_Match_Pct=4.0, sorted alphabetically by Company. Round both department averages to two decimals, set Satisfaction_Rating to High when the rounded Avg_Job_Satisfaction is at least 6.55 and Moderate otherwise, and sort Department alphabetically. For Health Insurance, PTO Days, and Retirement Match, compute the market average from competitors only and round it to one decimal; compute Gap=Our_Value-Market_Average rounded to one decimal. Set Priority to High for a negative gap, Medium for a gap from 0 through 1.0 inclusive, and Low for a gap above 1.0. Freeze the exact form questions and the seven observed department choices with this data.

From the verified canonical payload, the main agent starts the independent Form and workbook branches in native parallel. It is the sole owner of the Google Form. Call create_form exactly once with title Employee Benefits Improvement Survey, retain the returned formId, and sequentially add exactly these five required single-select multiple-choice questions:

1. Which department are you in? — choices are all seven department names from the verified department query.
2. How satisfied are you with current health insurance coverage? (1-5) — options 1, 2, 3, 4, 5.
3. How satisfied are you with current PTO policy? (1-5) — options 1, 2, 3, 4, 5.
4. How satisfied are you with retirement matching? (1-5) — options 1, 2, 3, 4, 5.
5. Which benefit improvement would you prioritize? — options Better Health Insurance, More PTO Days, Higher Retirement Match, Other.

Set required=true on every question; do not add an open-text question or substitute a checkbox question. Verify the title, exact question text, order, single-select types, options, and required flags through get_form. Do not retry an ambiguous form creation.

In the independent workbook branch, the main agent solely creates <agent_workspace>/Benefits_Analysis.xlsx with exactly these three sheets, writing all numeric values as literal numbers rather than formulas:

- Competitor Comparison: Company, Health_Insurance_Pct, PTO_Days, Retirement_Match_Pct; every competitor and Our Company, sorted by Company.
- Department Satisfaction: Department, Avg_Job_Satisfaction, Avg_Work_Life_Balance, Headcount, Satisfaction_Rating; the seven verified departments, rounded and rated as specified above, sorted by Department.
- Gap Analysis: Benefit_Category, Our_Value, Market_Average, Gap, Priority; one row for each of the three benefit categories using the frozen one-decimal averages/gaps and priorities.

Read every populated workbook range back and compare it with the canonical payload. After the form has been created and verified, the main agent may send the required email from the frozen gap analysis while the independent workbook branch finishes; it does not claim that the workbook is complete. Search Sent mail for exact subject Benefits Competitiveness Analysis & Survey Launch and recipient hr_leadership@company.com, paginating and reading candidates to verify the recipient and subject. Send once only if no exact match exists. The body must summarize the source-supported key benefits gaps and state that the employee survey has been created for additional input. Read the retained message back and verify the recipient, subject, and body; an ambiguous send is a blocker rather than permission to resend.

Run one final reconciliation turn covering the form ID and five required questions, the exact Benefits_Analysis.xlsx path and all three sheet read-backs, and the email ID/content. Only the main agent calls claim_done, after all three deliverables pass. Do not dispatch a sub-agent or add a verification wave.
