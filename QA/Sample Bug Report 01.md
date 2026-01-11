
SAMPLE-BUG-01 (High severity example)
Bug ID: BUG-01
Title: Invalid email submits without error
Environment: Chrome on macOS
Steps to Reproduce:
	1.	Open https://relocationroadmaps.com/
	2.	Enter test@ in the email field
	3.	Click Submit
Expected Result: Form should not submit. Email error should display.
Actual Result: Form submits and shows the success message.
Severity: High
Related Test Case: TC-04
Notes: Test fine, report for portfolio
