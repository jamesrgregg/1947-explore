## Risk Assessment 
The risk assessment evaluates the following:

_Maintenance_ - The evaluation looks at frequency of releases and if there have been any recent releases.  
 - Does the project have a release in the past 1.5 years (18 months)?
 - Does the project have a regular maintenance and patch cycle?
 - Does the project have maintainers? 
 - Is there a sense that the project has been orphaned? 
 
_Quality_ - The evaluation looks at the quality of coding practices, code reviews, static analysis, mailing list archives or forum submissions are all used to evaluate quality.
 - Is there quality development being done? 
 - What is the quality of code reviews? 
 - Is there evidence of a community that is showing responsiveness to Issues?
 - Does the project conduct code reviews of code changes?
 - Does the project utilize static code analysis?
 - Does the project currently have known high-severity security vulnerabilities or back doors that are have not been addressed in a reasonable time?

_Maturity_ - Older projects or components that have been well maintained usually have fewer security issues.
 - How long has the project existed?
 - Does the project have any CVEs against it?
 - How many lines of code per CVE for last 3 years? 
 - How does the project address CVEs?
 - Is there design and usage documentation (web, mail forums, books, email lists)?
 - Is there a documented test plan and test suites?
 - Is there evidence of community adoption?
 
_Support_ - The project is assessed for how bugs are reported and fixed, and if it has documented procedures for reporting security defects.
- Is there a way to submit security bugs or patches?
- Is there a documented security policy? 
- How widely used is this product?

## Acceptance Criteria for Approval / Rejection of Open Source Dependency
1. URL
    - Acceptance Criteria (Whitelist): 
        - URL of source code published
    - Rejection Criteria (Blacklist):
        - URL of source code unpublished
2. Documentation
    - Acceptance Criteria (Whitelist):
        - Project documentation published 
    - Rejection Criteria (Blacklist):
        - Project documentation unpublished
3. Maturity
    - Acceptance Criteria (Whitelist):
        - Project has history of active participation (e.g. commit history, response to issues, pull requests reviewed) over the course of the past 18 months
    - Rejection Criteria (Blacklist):
        - Project has no history of active participation (e.g. commit history, response to issues, pull requests reviewed) over hte course of the past 18 months
4. Contributors
    - Acceptance Criteria (Whitelist):
        - Project has current / active committers
    - Rejection Criteria (Blacklist):
        - Project has no current / active committers
5. Activity
    - Acceptance Criteria (Whitelist):
        - release cadence - project shows history of regular maintenance and patch schedule
        - recent commits as seen in github commit history
        - active dialog (Issues created and addressed / PRs created and actions taken to complete peer reviews)
    - Rejection Criteria (Blacklist):
        - The item isn't actively developed or maintained 
        - Small contributor count
        - Minimal update frequency
        - Lax review process
        - Minimal testing/documentation
        - No active vulnerability scanning
    - It does not use an OSI approved license https://opensource.org/licenses/alphabetical
    - It is not widely used or adopted
    - It has no CVE information 
        - Having no CVE information often means the tool hasn't been inspected from a security standpoint, not that it is 100% secure
6. Security
    - Acceptance Criteria (Whitelist):
        - Project has a process for reporting CVEs to the project contributors
        - Project has shown a history of responsiveness to addressing issues when there is a CVE reported
        - Announcements for known CVEs are reported publically
    - Rejection Criteria (Blacklist): 
        - Project has a no process for reporting CVEs to the project contributors
        - Project has shown no history of responsiveness to addressing issues when there is a CVE reported
        - No Announcements for known CVEs are reported or addressed
7. License
    - Acceptance Criteria (Whitelist):
    - Rejection Criteria (Blacklist):

## List of Soft Requirements (Other Considerations)
8. Forks
9. Followers
10. Stars
11. Other Considerations 
