
[source 1](https://www.synopsys.com/glossary/what-is-cicd.html#:~:text=CI%20and%20CD%20stand%20for,are%20made%20frequently%20and%20reliably.), [source 2](https://guvi.in/blog/continuous-integration-vs-continuous-deployment/), [source 3](https://medium.com/@ferhatsukrurende/continuous-integration-delivery-deployment-ci-cd-e1f3cbd14d5e), [source 4](https://katalon.com/resources-center/blog/continuous-delivery-vs-continuous-deployment), [source 5](https://youtu.be/h9K1NnqwUvE)

Small caveat: Ever wondered why I used "CI-CD" instead of "CI/CD", i.e., why use a hyphen (dash) instead of forward slash? 
Answer: Because I just try to avoid [some special characters](<https://www.quora.com/Which-special-character-should-be-avoided-when-naming-a-file#:~:text=%5C0%20(ASCII%20NULL,non%20ASCII%20charcters>) while writing headers, and to be easily [converted to markdown](https://stackoverflow.com/questions/43273842/what-are-the-rules-of-converting-one-markdown-title-into-an-html-anchor#:~:text=from%20the%20previous-,note,-.%0A1.All) if needed; just a habit I guess :.\].

# CI-CD Definition

#CI/CD 

* CI/CD stands for **C**ontinuous Integration and Continuous Delivery/Deployment. 
* CI/CD is a modern software development practice in which incremental code changes are made frequently and reliably ([s1](https://www.synopsys.com/glossary/what-is-cicd.html#:~:text=CI%20and%20CD%20stand%20for,are%20made%20frequently%20and%20reliably.)).
* CI/CD is how [DevOps](DevOps.md) automates the software release process.


![](Media-Temp/Pasted%20image%2020240122145135.png)

Adapted from [s5](https://youtu.be/h9K1NnqwUvE?t=888) . Note that I switched the locations of "Continuous delivery" and "continuous integration" since i think this logically more sense. More details on why I think this is the case are mentioned in [Continuous Integration vs Continuous Delivery vs Continuous Deployment](CI-CD.md#Continuous%20Integration%20vs%20Continuous%20Delivery%20vs%20Continuous%20Deployment).

## Continuous Integration vs Continuous Delivery vs Continuous Deployment

#continuous-integration #continuous-delivery  #continuous-deployment

![](Media-Temp/Pasted%20image%2020240122141101.png)

([s2](https://www.guvi.in/blog/continuous-integration-vs-continuous-deployment/#:~:text=principles%20of%20CI.-,Both,-CI%20and%20CD))

Side note: The diagram above represents the [DevOps](DevOps.md) steps except the first one: "plan".

Differences:

Continuous Integration (CI) is a software development practice where ([s2](<https://www.guvi.in/blog/continuous-integration-vs-continuous-deployment/#:~:text=the%20DevOps%20way.-,Continuous%20Integration,-(CI)>)):
* Developers frequently merge their code changes into a central repository.
* Other aspects of a CI process ([s5](https://youtu.be/h9K1NnqwUvE?t=1146)):
  
  ![|500](Media-Temp/Pasted%20image%2020240122150402.png)
  
* Integrations are then verified by an automated build and automated tests ([s5](https://youtu.be/h9K1NnqwUvE?t=1179)):
  
  ![|450](Media-Temp/Pasted%20image%2020240122150151.png)
  
* A buildable-runnable version is produced from CI ([s3](https://medium.com/@ferhatsukrurende/continuous-integration-delivery-deployment-ci-cd-e1f3cbd14d5e#:~:text=A%20buildable%2Drunnable%20version)).


Continuous Delivery (CD) allows testing of the business logic ([s3](https://medium.com/@SaviantConsulting/continuous-integration-vs-continuous-delivery-vs-continuous-deployment-60e96e9a7a08#:~:text=CD%20allows%20testing%20of%20the%20business%20logic.)) to ensure that the software is always release-ready <mark style="background: #D2B3FFA6;">with manual approval</mark> ([s4](https://katalon.com/resources-center/blog/continuous-delivery-vs-continuous-deployment#:~:text=Simply%20put%2C%20Continuous%20Delivery%20focuses%20on%20ensuring%20software%20is%20always%20release%2Dready%20with%20manual%20approval%2C%20while%20Continuous%20Deployment%20automates%20the%20release%20process%2C%20deploying%20changes%20to%20production%20automatically%20once%20tests%20pass.)).


Continuous Deployment is the same as Continuous Delivery, but <mark style="background: #D2B3FFA6;">with automated approval</mark>; Once tests are passed, the software is automatically deployed to the production environment ([s4](https://katalon.com/resources-center/blog/continuous-delivery-vs-continuous-deployment#:~:text=Simply%20put%2C%20Continuous%20Delivery%20focuses%20on%20ensuring%20software%20is%20always%20release%2Dready%20with%20manual%20approval%2C%20while%20Continuous%20Deployment%20automates%20the%20release%20process%2C%20deploying%20changes%20to%20production%20automatically%20once%20tests%20pass.)). 


