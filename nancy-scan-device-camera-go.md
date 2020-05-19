 - Use within local development workflow
 - Use within CI - Jenkins build as part of the PR build, include a stage to run `nancy`

```
go list -m all | docker run -i sonatypecommunity/nancy:latest

```


![Nancy Scan](/images/nancy-1.png)

![Nancy Scan](/images/nancy-2.png)

![Nancy Scan](/images/nancy-3.png)
