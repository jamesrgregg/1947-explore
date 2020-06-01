# Issue 1947-Explore

Table of Contents
 - [Problem Statement](#problem-statement)
 - [Current Process](#current-process) 
 - [Ideal Process](#ideal-process)
 - [Approach](approach.md)
 - [Research](research.md)
 - [Additional Considerations](additional-considerations.md)
 - [Summary of Findings and Final Recommendation](#summary-of-findings-and-final-recommendation)


## Problem Statement
The project does not have an objective means of evaluating the security of 3rd party components as they are being introduced to the EdgeX Foundry code base. A recent pull request introduced a 3rd party component, GoKey, to be used in password generation. No formal assessment was done of the library before deciding to include it as part of a security-critical flow.

This proposal is presented as an approach to present options to the EdgeX Foundry Security Working Group.  This work is submitted for consideration of multiple options with a phased approach as outlined in [Issue #1947][15] - _crawl_, _walk_, _jog_, _run_ with the goal of implementing the best possible option for Hanoi scope of work  - October 2020 release timeframe.

## Current Process
Someone researches the open source component that is desired, sometimes after the code has already been integrated into the EdgeX Project, without completion of any formal review.

The current high-level statistics are used in the manual research process (e.g. paper study) are:

```
Age: Age of the Open Source Project
Commits: Count - Total Commits
Issues: Count - Open Issues / Closed Issues
Releases: Count - Releases
Stars: Count - Stars
Forks: Count - Forks
Watchers: Count - Watchers
CVEs: Count - CVEs (query NVD database)
Other Criteria: Subjective Assessment of Reviewer
```

## Ideal Process
This request proposes the development of an objective process for assessing the security risk of 3rd party components. Such a process could take into consideration item such as the project's age, popularity / maturity, evidence of security practices, recent commit history, diversity of committers, established CVE practices, or other observable evidence.

Ideal process would include consideration of:
 - Data acquisition via automation
 - Disposition based on policy
 - Consideration of BKMs from other OSS projects
 - Assessment of overall maturity / health / ongoing current development by the OSS community
 - Assessment of known CVEs for code and dependencies

 Additionally, the ideal process should take into account the following scenarios:
 
 1. Existing Code (Skeletons in the Closet)   
 2. Code in Holding (Analysis of code before it is accepted)
 3. Pull Request with new dependency

## Summary of Findings and Final Recommendation
| Use Case | Process | Tools | Applicability |
|---|---|---|---|
| 1.) Existing Code (Skeletons in the Closet)|Automated scan within build automation via Snyk CLI|Snyk / Clair / Community Bridge Advanced Snyk Reports| Scan automation occurs within the build - PR merge to master |
| 2.) Code in Holding (Analysis of code before it is accepted) |Submitter adds a [DepShield][6] banner to the README and includes scan findings for consideration as part of the code review.  Scan results should consider license information and CVE data. | At a bare minimum, project dependencies can be assessed via any of the following: [OpenHub][17], [NVD Vulnerability Search][18], [Snyk CLI][19], [Dependency-Check CLI][20], [Nancy CLI (Sonatype)][8] |When considering code that is under consideration for moving into the main EdgeX Foundry Org |
| 3.) Pull Request with new dependency | Update Pull Request template to include check box indicator for changes to go module dependencies.  Add a `dependency` label to the pull request.  Reviewer will see one of the changed files is go.mod.  PR can include reference to scan results (Snyk) that can be referrenced by looking at the Pipeline.| Pull Request Template / GitHub label / Snyk / Clair / Community Bridge Advanced Snyk Reports | On a Pull Request, whenever there's a new dependency introduced as shown through changes to the go.mod|

The modification of the Pull Request template and the addition of a `dependency` label is easily completed within the Hanoi scope of work.  The automation using Snyk and the supplimental Advanced Snyk Reports is already in place.



[1]: https://www.fossology.org/ "Fossology"

[2]: https://owasp.org/www-project-dependency-track/ "Dependency Track" 

[3]: https://www.sonatype.com/press-release-blog/sonatype-goes-long-with-godelivers-fully-automated-security-solution-for-fast-growing-programming-language "Sonatype - Nexus IQ"

[4]: https://www.sonatype.com/hubfs/eBooks/AHC_Guide.pdf

[5]: https://guides.sonatype.com/repo3/technical-guides/go-dependencies-nxrm3/

[6]: https://www.sonatype.com/depshield

[7]: https://ossindex.sonatype.org/

[8]: https://github.com/sonatype-nexus-community/nancy

[9]: https://goalie.dev/

[10]: https://securitylab.github.com/tools/codeql](https://securitylab.github.com/tools/codeql) "CloudQL"

[11]: https://vimeo.com/213230554/cf3893517c

[12]: https://travis-ci.org/github/sonatype-nexus-community/intentionally-vulnerable-golang-project/builds/490260408

[13]: https://help.sonatype.com/integrations/nexus-and-continuous-integration/nexus-platform-plugin-for-jenkins#NexusPlatformPluginforJenkins-ConnectingJenkinstoIQServer

[14]: paper-study.md

[15]: https://github.com/edgexfoundry/edgex-go/issues/1947

[16]: nancy-scan-device-camera-go.md

[17]: https://openhub.net

[18]: https://nvd.nist.gov/vuln/search

[19]: https://support.snyk.io/hc/en-us/categories/360000456217-Snyk-CLI

[20]: https://jeremylong.github.io/DependencyCheck/dependency-check-cli/index.html

[21]: https://github.com/marketplace/actions/file-changes-action

[22]: https://support.snyk.io/hc/en-us/articles/360000897917-What-counts-as-a-test-

