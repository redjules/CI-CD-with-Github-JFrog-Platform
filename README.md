# CI-CD-with-Github-JFrog-Platform

<img width="909" alt="Screenshot 2024-09-19 at 22 50 58" src="https://github.com/user-attachments/assets/df7e9652-78a1-441b-999a-bb3ed7fbaf06">


<img width="879" alt="Screenshot 2024-09-19 at 22 51 56" src="https://github.com/user-attachments/assets/d74845bf-2707-427e-b96e-9249671d2d71">

<img width="760" alt="Screenshot 2024-09-19 at 22 53 30" src="https://github.com/user-attachments/assets/bfe8a7f6-8e4a-4039-8d5c-c656cfff8342">

We have here a springboard application, a beta feature:

![Screenshot 2024-09-19 at 23 20 48](https://github.com/user-attachments/assets/a4060eba-2f03-4483-b439-dd3dfc904e1e)

if you go to feature manager in Azure and turn that off

<img width="593" alt="Screenshot 2024-09-19 at 23 16 54" src="https://github.com/user-attachments/assets/68fd7f92-3c32-4e0b-95e5-4ee7dbac08a8">

and go back to the website and refresh, the feature is gone: 

<img width="656" alt="Screenshot 2024-09-19 at 23 17 08" src="https://github.com/user-attachments/assets/3d1c521a-b53a-4059-8e3c-d0ea0c276190">


to create this web app:

<img width="430" alt="Screenshot 2024-09-19 at 22 53 43" src="https://github.com/user-attachments/assets/2beb64b6-9f1d-4bb1-9418-8908c6bea78d">


<img width="674" alt="Screenshot 2024-09-19 at 22 54 19" src="https://github.com/user-attachments/assets/859fa017-d5e8-471a-b7e5-c4ab0e4454eb">

we enable continuous deployment:


<img width="653" alt="Screenshot 2024-09-19 at 22 54 50" src="https://github.com/user-attachments/assets/c7ccc965-b83c-40a2-b47f-47ae0c5454ba">

<img width="695" alt="Screenshot 2024-09-19 at 22 55 18" src="https://github.com/user-attachments/assets/d5a1f4e4-5eba-4a07-a7ab-6af7ea030c3b">


it creates a yaml (Preview):

<img width="809" alt="Screenshot 2024-09-19 at 22 55 40" src="https://github.com/user-attachments/assets/4d377dfd-1412-4212-8bee-40bd9702b09e">

<img width="624" alt="Screenshot 2024-09-19 at 22 56 45" src="https://github.com/user-attachments/assets/7d6e8325-d345-4568-ad94-61d0a4ee8f27">

<img width="494" alt="Screenshot 2024-09-19 at 22 57 20" src="https://github.com/user-attachments/assets/1cad65fb-fcae-4e97-b863-889c3f1ad49e">

go to settings and secrets in github:

<img width="877" alt="Screenshot 2024-09-19 at 22 57 47" src="https://github.com/user-attachments/assets/61f6d607-421d-43e1-a16e-3a88ddcb8b8c">

the settings.xml has info you don't necessarily want to pass in, like passwords so you can use Artifactory password:

<img width="666" alt="Screenshot 2024-09-19 at 22 58 34" src="https://github.com/user-attachments/assets/fdabf4b5-45d1-4976-8434-ee10df6385a6">

<img width="699" alt="Screenshot 2024-09-19 at 22 59 33" src="https://github.com/user-attachments/assets/1b536854-84bd-4750-8b1b-6838e1498e81">

these secrets appear in the workflows, main yaml but this time are environment variables:

<img width="468" alt="Screenshot 2024-09-19 at 23 01 11" src="https://github.com/user-attachments/assets/8f8c0714-a44b-4966-b0d2-83e3b17f65a4">


<img width="400" alt="Screenshot 2024-09-19 at 23 00 29" src="https://github.com/user-attachments/assets/fa161825-c44b-44ba-8cce-d2ae41e43827">

<img width="351" alt="Screenshot 2024-09-19 at 23 03 06" src="https://github.com/user-attachments/assets/8a79ff58-7533-4b20-a32c-948d404f4117">

the build goes and because the connection string and the published profile, it creates a target jar file and from there you can pick a deployment task which passes that jar file to the Azure Web App, puts it in the right place and runs the web app

<img width="498" alt="Screenshot 2024-09-19 at 23 04 40" src="https://github.com/user-attachments/assets/9e2e7a9f-198a-48e8-a22d-a734dde2c2da">


<img width="254" alt="Screenshot 2024-09-19 at 23 04 59" src="https://github.com/user-attachments/assets/f79c3ec1-096f-47cb-8422-24ced3773938">

and you have the feature

<img width="537" alt="Screenshot 2024-09-19 at 23 05 27" src="https://github.com/user-attachments/assets/a072be50-47c2-4e4f-87ed-e82b62601dac">

So you go in, you generate the automatic yaml, oncethe yaml fails because first time it doesn't have the environment variables set up, you update the yaml file for the workflow and you're setting XML with artifactory data. Once it runsyou can see here in the Jfrog platform all the artifacts that got stored automatically in Artifactory

![Screenshot 2024-09-19 at 23 18 56](https://github.com/user-attachments/assets/376ab276-9b29-44f5-b2c1-348a46409850)


<img width="503" alt="Screenshot 2024-09-19 at 23 08 01" src="https://github.com/user-attachments/assets/6eb9a4fc-bb9a-4f17-bd1b-3e7e3fde50ef">

what artifactory does for you is it provides you a proxy so when you need to collect those artifacts it will proxy that request out to Maven Central.

This project was set up to point to the Artifactory instance

![Screenshot 2024-09-19 at 23 19 34](https://github.com/user-attachments/assets/97000cf0-6165-443a-ac65-5cfa8f80e348)


when you ask for an artifact that Artifactory doesn't have yet, and you pull that out from Maven Central that initial request is pulling that artifact in from Maven Central adn the subsequent requests are gonna pull from that artifactory instance. There are several reasons to do that: performance reasons, security reasons if are behind a firewall and you don't have direct access to the Internet and those public repos.
