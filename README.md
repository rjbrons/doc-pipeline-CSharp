# Code Pipeline for C#
## Files for the C# Application folder
1.	Fork the readme and test repo <br>
2.	Make sure it works locally<br>
a. 	If you don’t have dotnet project fork it from the following repo (https://github.com/thatsjustjohn/deployment-app-csharp)<br>
b.	To test locally if you need the dotnet-sdk below are the commands for mac<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i.	`brew update`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ii.	`brew tap caskroom/cask`<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;iii.	`brew cask install dotnet-sdk `<br>
3.	Run `dotnet build` command to build the application.
4.	Run `dotnet run` –project <project name> to start the server.
5.	Run `dotnet test` to run the preconfigured tests for the application.
6.	From inside the application directory run ` zip -r -X site.zip .` to zip the application for uploading to elastic beanstalk.
7.	Verify that there is an buildspec.yml is at the base level and there is a basic-web-app/aws-windows-deployment-manifest.json

# Elastic beanstalk 
Now that the application is running locally lets move this to AWS
1.	Create a new environment in Elastic beanstalk<br>
a.	Application name – name of the application<br>
b.	Create a new environment<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i.	Select web server environment<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ii.	Select .Net from the Preconfigured platform<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;iii. Upload the application zip file<br>
c.	Verify that your application is deployed and accessible from the elastic beanstalk link.<br>
d.	If there are issues check your buildspec.yml and aws-windows-deployment-manifest.json files.<br>

# Code Pipeline
1.	Click create pipeline in CodePipeline <br>
2.	On pipeline settings, enter pipeline name. Click next.<br>
3.	Under source provider, select Github and connect to github. Enter credentials.<br>
4.	Select repository and master branch, then click next.<br>
5.	Build <br>
a.	Build provider – AWS Codebuild<br>
b.	Region – default <br>
c.	Project – Click create project <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i.	Under Create a build Project <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Enter Project Name <br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Select managed image <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Select Operating system <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Runtime – Standard <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Image – Select Standard 2.0 <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Image version – Select Always use the latest image for this runtime version <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Select new service role <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Buildspec - insert build command - `dotnet test && dotnet build` <br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Click continue to code pipeline <br>
6.	Add Deploy Stage<br>
a.	Deploy provider – AWS Elastic Beanstalk<br>
b.	Region – default<br>
c.	Application name – Elastic beanstalk application name<br>
d.	Environment name – Elastic beanstalk environment name<br>
e.	After reviewing Click create pipeline<br>

## Potential roadblocks or trouble spots
During Build
YAML_FILE_ERROR Message: This build image requires selecting at least one runtime version.

During Deploy
The action failed because either the artifact or the Amazon S3 bucket could not be found. Name of artifact bucket: codepipeline-us-west-2-662875121028. Verify that this bucket exists. If it exists, check the life cycle policy, then try releasing a change.

## Link to Deployed website


## Link to GitHub
- https://github.com/thatsjustjohn/deployment-app-csharp

## Group:
* John Winters
* Kush Shrestha
* Robert Bronson
* Luke Chandler

