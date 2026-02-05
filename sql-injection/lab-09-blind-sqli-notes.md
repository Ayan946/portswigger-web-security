# Blind SQL Injection – Learning Notes

## Context
Today I started working on the Blind SQL Injection labs from the PortSwigger Web Security Academy.
Unlike classic SQL injection, Blind SQL injection does not directly return query results in the application response.

## What Makes Blind SQL Injection Different
- No visible database errors or data output
- Exploitation relies on application behavior changes
- Requires logical conditions to infer true or false responses

## Techniques Involved (High Level)
- Conditional responses (true/false behavior)
- Boolean-based inference
- Time-based inference (in some cases)

## Challenges
- Requires careful observation of application behavior
- Slower and more methodical than UNION-based SQL injection
- Easy to make logical mistakes without structured testing

## Current Status
⏳ In progress — actively working on completing the lab.

## Key Takeaway So Far
Blind SQL injection highlights how dangerous insecure query construction can be, even when no data is visibly returned to the user.
