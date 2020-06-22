## Tool Comparison FOSSA and Snyk
FOSSA is a young start up at this point in time.  They started out as a compliance company and mostly focused on software legal compliance - licensing.  They have an Enterprise product offering that includes security vulnerability scanning.  FOSSA doesn't publicly disclose what databases they integrate with as the source of their scan data.  

There's a Q2 2019 Forrester Wave report that lists the following in summary:
 - WhiteSource and Synopsys topped the list of leaders (Leaders) of the market;
 - Snyk and Sonatype are named Strong Performers;
 - WhiteHat Security , Flexera and Veracode are called Contenders;
 - GitLab , FOSSA and JFrog are Challengers.

The have a CLI that could be integrated with CI/CD, except that they don't yet offer a public Docker image of their CLI.  The current product lacks container and serverless scanning capabilities.

Scan data does not make sense as the findings don't reveal any detail of where a vulnerable component is being used in the code.  The software is buggy with errors observed in the FOSSA portal when loading data on the page.

The dependency count for edgex-go is shown as 6510 dependencies vs. 121 within Community Bridge Advanced Snyk Reporting provided by the Linux Foundation.  FOSSA seems to have identified npm package dependencies for the project which is written in Go.

FOSSA would require someone to take action with in the dashboard and given the findings and the lack of guidance that the product offers, it would seem almost an impossible task.  This would be considered a `heavy lift` for anyone on the project.  It would equate to more work and less feature developmenmt for the project.  The product does not offer advise to developers on how to remediate vulnerabilites.  It does not recommend fixes.  

Snyk not only has a CLI but has been fully Dockerized and has been successfully integrated into the EdgeX Foundry build pipelines since the Fuji release.  The product offers insight into remediation and has integration with reporting that comes via dashboard, Slack and email notification.  The Advanced Snyk Reports made available through the Linux Foundation Community Bridge offers additional insights that can be reviewed for detail such as licensing and dependencies.  The ability to integrate with multiple 3rd party tools such as GitHub, Docker Hub, Nexus, Slack, Jira, is a benefit over what comes out of the box with FOSSA.  The feedback loop for developers is almost immediate within the CI/CD pipelines.  That combined with weekly and ongoing notifications, keeps the developers advised of any new vulnerabilities when found.  Snyk along with the Community Bridge Advanced Snyk reports is good enough for the project at this time.  In terms of effort needed to support Snyk, it's minimal in comparison to what it would take to support FOSSA.


