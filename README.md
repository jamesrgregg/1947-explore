## Problem Statement
The project does not have an objective means of evaluating the security of 3rd party components as they are being introduced to the EdgeX Foundry code base. A recent pull request introduced a 3rd party component, GoKey, to be used in password generation. No formal assessment was done of the library before deciding to include it as part of a security-critical flow.

This proposal is presented as an approach to present options to the EdgeX Foundry Security Working Group.  This work is submitted for consideration of multiple options with a phased approach as outlined in [Issue #1947][15] - _crawl_, _walk_, _run_ with the goal of implementing the best possible option for Hanoi scope of work  - November 2020 release timeframe.

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

## Proposed Approach (Crawl, Walk, Run Slow, Run Fast)

**_Crawl:_** 

Proposal: Paper study (manual) as completed previously.  Submission of the paper study to a working group for review within the working group via Pull Request

Applicability: Applies to both consideration within review before moving out of holding repo as well as main org

Time / Frequency: As needed or requested by EdgeX WG chairs

**_Walk:_** 

Proposal: Automation of paper study to include all required data points - scope includes automating the generation of the report (ad-hoc) + use of Community Bridge Advanced Snyk reporting AS-IS

Applicability: Applies to both consideration within review before moving out of holding repo as well as main org

Time / Frequency: As needed (ad-hoc) or as requested by EdgeX WG chairs

**_Slow Run:_** 

Proposal: Combination of the automated paper study + [Fossology][1] (with generation of evidence collected / considered) + use of Community Bridge Advanced Snyk reporting (issues fixed) as a stretch goal

Applicability: Applies to both consideration within review before moving out of holding repo as well as main org

Time / Frequency: As needed (ad-hoc) or as requested by EdgeX WG chairs

**_Fast Run_**: 

Proposal: Combination of automated paper study + [Fossology][1] + [Dependency Track][2] or similar (Sonatype - Nexus IQ - See Note)

 - Requires explore with LF to see what may exist already

 - Requires explore of landing a dedicated solution of [Dependency Track][2] on Linux Foundation infrastructure

Note: Linux Foundation has [Sonatype - Nexus IQ][3]
Applicability: Applies to both consideration within review before moving out of holding repo as well as main org

Time / Frequency: As needed (ad-hoc) or as requested by EdgeX WG chairs

## Research
### Paper Study (_crawl_)
Continue the manual research process ad-hoc with review within the working group.
 - Assumes manual process is good enough 
 - Requires periodic reassessment with no set schedule

### Automated Paper Study (_walk_)

Scan GitHub repos as defined by a list of projects with queries defined to pull last 5 years of data.  Would require definition of the required metrics.  
Current script pulls data on 20 data points
1. Existence of a README beyond a one-liner (evidence of project maturity) + Link
2. Tags (Count) + Link
3. Releases (Count) + Link
4. Pull Requests (Count) + Link
5. Commits (Count) + Link
6. Open Issues (Count) + Link
7. Closed Issues (Count) + Link
8. Open Security Issues (Count) + Link
9. Closed Security Issues (Count) + Link
10. Project Org / Project Name

Example: [Automated Paper Study][14]

Note: Does not currently include all of the data points which were included in the manual paper study (missing stars, forks, watchers,known vulnerabilities as per NVD)

### Community Bridge - Advanced Snyk Reporting (_slow run_)

Community bridge - Advanced Snyk Reporting is already set up with access to Security Working Group (EdgeX SIR Team)
 - Includes all of the dependencies included in the project as defined by go.mod file
 - Includes License 
 - Data extract does not include License
![Community Bridge](/images/cb-snyk.png)
 - Dependency Tree view displays nested dependencies and license
 - Doesn't always show details
 - Unknown licenses identified for several components
 ![Dependency Tree](/images/cb-snyk-deptree.png) 

Community Bridge Team working on enhancements to the UI with plans to provide a separate tab to navigate license dependency for different repositories.



### FOSSology (_not recommended for EdgeX Foundry_)
FOSSology is a open source license compliance software system and toolkit. As a toolkit you can run license, copyright and export control scans from the command line. As a system, a database and web ui are provided to give you a compliance workflow. License, copyright and export scanners are tools available to help with your compliance activities.

[Basic Workflow](https://www.fossology.org/get-started/basic-workflow/) 
 - Very manual process required for recording of decisions of review
 - Requires a version of FOSSology to be running accessible / long lived with persistent storage of project database
 - Someone would perform the analysis and disposition of every license within the project
 - Requires deep knowledge of compliance related to licensing, copyright law, ECC etc..
 ![FOSSology](/images/fossology.png)

#### Definition of Done
Check for all of the following:
1. All licenses are checked?
2. All copyrights are checked?
3. ECC information is checked ?
4. Main license is selected?
5. Reviewed files for irrelevant sections?

### Dependency-Track (_not recommended for EdgeX Foundry_)
Dependency-Track is an intelligent Supply Chain Component Analysis platform that allows organizations to identify and reduce risk from the use of third-party and open source components. Dependency-Track takes a unique and highly beneficial approach by leveraging the capabilities of Software Bill-of-Materials (SBOM). This approach provides capabilities that traditional Software Composition Analysis (SCA) solutions cannot achieve.

Dependency-Track monitors component usage across all versions of every application in its portfolio in order to proactively identify risk across an organization. The platform has an API-first design and is ideal for use in Continuous Integration (CI) and Continuous Delivery (CD) environments.
![Dependency-Track](/images/dependency-track.png)

Findings: Installed locally via Docker image and noted did not work as expected so continued explore with Linux Foundation and found they offer Nexus IQ.

### Sonatype - NexusIQ
The Linux Foundation offers Nexus IQ to the community - Free. 

Support for Go, Java, PHP, JavaScript and other languages.

Would require project to adopt use of go.sum files which were previously not allowed because of the problems we encountered in the JJB Freestyle Jenkins jobs.  Per Trevor..."We found the Go team sometimes changed the manner in which hashes within the go.sum were calculated between patch versions. The hashes are used to identify a specific version of a dependency. This caused a problem whereby if a dev had a later patch version of Go on their box than what was in the build pipeline, our build env wouldn't know how to resolve the dependency versions on a verify job."
![Sonatype - Nexus IQ](/images/sonatype.png)


[Go Application Analysis](https://help.sonatype.com/iqserver/analysis/go-application-analysis)


 - Supports Policy Evaluation using [Nexus Platform Plugin][11]

 - Supports use within Build Automation [Sonatype - CI Build Automation Output][12]

 - Documentation looks good with Pipeline syntax examples [Connecting Jenkins to Nexus IQ][13]

 - Support for Slack integration via webhooks

 - Supports container scanning / Docker image scans like Clair / Snyk

 ```
Steps
Open your CLI, and enter the following commands:

1. Pull the Docker image: Docker pull webgoat/webgoat-7.1
2. Save the image as a tar file: Docker save webgoat/webgoat-7.1:latest > webgoat-7.1.tar
3. Run the scan from the Nexus IQ CLI: 
java -jar ./nexus-iq-cli-1.59.0-01.jar -i dockerapp -s http://localhost:8070 -a admin:changeme -t build webgoat- 7.1.tar

```

Note: Need to check if Linux Foundation has the license to support integration via plugin.

## References

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

## Additional Considerations

### Free Tools
For individual developers or organizations just getting started with open source governance, Sonatype also offers a suite of free tools including: 

[Nexus Vulnerability Scanner][4] - scans Go apps and creates a software bill of materials. 

[Nexus Repository Manager OSS][5] - proxy and manage Go binaries.

[DepShield][6] - uses OSS Index to check for vulnerabilities in your Go dependencies at the commit level within GitHub. 

[OSS Index][7] - free service used by developers to identify open source dependencies and determine if there are any known, publicly disclosed, vulnerabilities. 

[Nancy][8] - uses OSS Index to identify vulnerabilities in Go dependencies. Nancy is available in GitHub, but does not have access to commits. Nancy runs on a private project or local machine. 

[Goalie][9] - scans binaries against OSS Index data to identify component-level vulnerabilities.