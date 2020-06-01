## Additional Considerations

### Free Tools
For individual developers or organizations just getting started with open source governance, Sonatype also offers a suite of free tools including: 

[Nexus Vulnerability Scanner][4] - scans Go apps and creates a software bill of materials. 

[Nexus Repository Manager OSS][5] - proxy and manage Go binaries.

[DepShield][6] - uses OSS Index to check for vulnerabilities in your Go dependencies at the commit level within GitHub. This could be an option for vetting Go, Java, JavasScript and others
Sonatype DepShield is a GitHub App used by developers to identify and remediate vulnerabilities in their open source dependencies.  DepShield will monitor your project's dependencies for publicly disclosed security vulnerabilities and alert you natively in GitHub when they are discovered.  Security vulnerability data is powered by Sonatype OSS Index, a free service used by developers to identify open source dependencies and determine if there are any known, publicly disclosed, vulnerabilities.

There's a GitHub bot that can be used for dependency management that gives insight at the repo level and automatically opens up Issues when a new publically disclosed security vulnerability is found.  [Sonatype DepShield on GitHub Marketplace](https://github.com/marketplace/sonatype-depshield)

Adding a DepShield badge to a repo would allow for the visualization of findings of components with a count of known vulnerabilities.  In terms of the use cases which require spot check that include the consideration of some of the metrics considered in the paper study, this might be a means to identify where the project needs to spend some time to address findings identified as either _high_ / _medium_. 
As a step to look at this closer, I forked the device-camera-go repo and added a DepShield badge.  The [results](https://github.com/jamesrgregg/device-camera-go/blob/master/Readme.md) are immediately observed after adding the badge.  A deeper dive with a scan would be required to know what component may need to be addressed.  

Note: This results displayed in the DepShield badge, is without any integration to any additional tooling.

[OSS Index][7] - free service used by developers to identify open source dependencies and determine if there are any known, publicly disclosed, vulnerabilities. 
There is a REST API exposed for requesting component vulnerability reports.
The REST API specification is available via [Swagger](https://ossindex.sonatype.org/rest) interface for more details. 

[Nancy][8] - uses OSS Index to identify vulnerabilities in Go dependencies. Nancy is available in GitHub, but does not have access to commits. Nancy runs on a private project or local machine. 
Reference: [Nancy Scan Example of device-camera-go][16]

[Goalie][9] - scans binaries against OSS Index data to identify component-level vulnerabilities.

[Dependabot Preview](https://github.com/marketplace/dependabot-preview)
Dependabot aggregates everyone's test results into a compatibility score, so you can be certain a dependency update is backwards compatible and bug-free.

Dependabot monitors security advisories for Ruby, JavaScript, PHP, Java, .NET, Python, Elixir and Rust. The bot will automatically create PRs immediately in response to new advisories.

Note: Dependabot is in _preview_ and does not include security advisories for all languages (missing support for Go).  It was also noted during the Architect's discussion on 05/18/2020, that the review of dependencies is orthogonal to the decisions that needed for this scope.

[NVD Database](https://nvd.nist.gov/vuln/search) - Search the NVD Database 
based on product name, vendor name, CVE name or an OVAL query.
```
curl -s https://services.nvd.nist.gov/rest/json/cves/1.0?keyword=expressjs| jq '.totalResults'
1
```


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

