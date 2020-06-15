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

### Community Bridge - Advanced Snyk Reporting (_jog_)

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

In terms of the work involved and the requirement for having a dedicated community member who would complete the analysis, the use of this tooling is considered a `Heavy Lift` and not recommended for the project.

### Dependency-Track (_not recommended for EdgeX Foundry_)
Dependency-Track is an intelligent Supply Chain Component Analysis platform that allows organizations to identify and reduce risk from the use of third-party and open source components. Dependency-Track takes a unique and highly beneficial approach by leveraging the capabilities of Software Bill-of-Materials (SBOM). This approach provides capabilities that traditional Software Composition Analysis (SCA) solutions cannot achieve.

Dependency-Track monitors component usage across all versions of every application in its portfolio in order to proactively identify risk across an organization. The platform has an API-first design and is ideal for use in Continuous Integration (CI) and Continuous Delivery (CD) environments.
![Dependency-Track](/images/dependency-track.png)

Findings: Installed locally via Docker image and noted several issues where it did not work as expected.  Decided to continue explore with Linux Foundation.

In terms of the work involved and the requirement for having a dedicated community member who would complete the analysis, the use of this tooling is considered a `Heavy Lift` and not recommended for the project.
Additionally, this solution would require dedicated infrastructure and coordination with the Linux Foundation.  

### Sonatype - NexusIQ (_not recommended for EdgeX Foundry_)
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
 - Report does include License Analysis 

Per the explore with Linux Foundation, most of the projects are already registered in Nexus IQ since it's part of the Java jobs in global-jjb.  Only a subset (3) of the projects are actively utilizing Nexus IQ, none of which are Go based projects.
 - Requires additional explore (deep dive) and assess ease of integration with Nexus IQ offering.
 - Requires consideration of extra burden on developers to maintain both go.sum and go.mod files within each repo.
 - Assumes integration via Jenkins Plugin is included in the service offering

As per discussion in DevOps WG, the decision was made to discontinue the continued explore of Nexus IQ given that the project does not commit the go.sum file to the repos for multiple reasons.

## FOSSA
FOSSA software is Open Source Management for Enterprise Teams.  It looks at end-to-end management for 3rd party code, license compliance, and vulnerabilities.

Software might be better suited for projects with a high level of maturity and where the project is at the point that there's a recognition for the need of an Open Source Program Office (OSPO).

### Initial findings from two EdgeX projects (forks)
![FOSSA](/images/fossa-dashboard.png)

## Deep Dependency Analysis (scan depth of 5 dependencies)
![FOSSA Dependencies](/images/fossa-dependencies.png)

## License Compliance
License scan banner status message shows failing for edgex-go
Free plan does not go down the rabbit hole far enough to see the transitive dependencies' licenses.
![](/images/fossa-licenses-edgex-go.png)





## Additional Options
No suitable bot was discovered for this explore, however there is a GitHub Action, [file-changes-action][21] that could be leveraged with further explore.  It should be noted however, the results of the action are not much more than a log for review, and the PR itself gives similar changed file indicators via better visualization.

Also, the Snyk scans were limited in the Jenkins Pipelines to only scan when PR merged to master.  Given the pricing model where public open source projects are [unlimited and free][22], we can change the Jenkins Pipelines to scan on every PR, however it's not necessary unless the community was looking to take action for immediate remediation whenever there was a finding and in order to do so, we would have to modify the builds to break when there is a finding.

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

