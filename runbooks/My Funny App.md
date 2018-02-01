# My Funny App Demo
This file describes the default workflow of My Funny App, which is based on Python. In my example  a Docker Enterprise Standard Demo.

#Prerequisites
1. An up and running Docker Enterprise Edition (UCP and DTR incl. HRM configuration) either on-prim or in the cloud. 

    Hint: This demo was tested with Docker Engine 17.06.2-ee-5, UCP 2.2.4 and DTR 2.4.9
2. Use git and clone this repository to your local host. 

    "$ git clone https://github.com/automatecloud/docker-ee-demos.git"

    You now have the necessary demo code on your worker host.

#Demo Steps

1. Change into the linux_tweet_app directory.

    - "cd ./docker-ee-demo/dockerfiles/my-funny-app/"

2. Build a container of my-funny-app with tag "1.0".

    - "docker build -t <dtrfqdn>/my-funny-app:1.0 ."

3. Build a contaner of my-funny-app with tag "broken".

    - modify HEALTHCHECK reference in Dockerfile to HEALTHCHECK CMD curl --fail http://localhost:500 || exit 1 
    - "docker build -t <dtrfqdn>/my-funny-app:broken ."

4. Build a container of my-funny-app with tag "2.0".

    - modify index.html file by changing the background color #127ab1 to #00008B darkblue
    - change HEALTHCHECK reference in Dockerfile to HEALTHCHECK CMD curl --fail http://localhost:5000 || exit 1
    - docker build -t <dtrfqdn>/my-funny-app:2.0 .

5. Create a my-funny-app repository in the DTR.

6. Login to your DTR on your local machine and push all three images to the in step 5 created repository

    - docker login <dtrfqdn> (you will be asked for user and password, please provide as appropriate)
    - docker push <dtrfqdn>/my-funny-app:1.0
    - docker push <dtrfqdn>/my-funny-app:broken
    - docker push <dtrfqdn>/my-funny-app:2.0

7. Create my-funny-app stack on UCP with ucp-bundle.

    - change to the ucp-bundle folder
    - eval $(<env.sh)
    - docker stack deploy --compose-file /home/gitlab-runner/my-funny-app-1.0.yml my-funny-app
    - Login to the UCP UI and check the service is up and running 
    - Connect to the published address of this page

    Hint: 
    
    - How to obtain and install the ucp-bundle on your local engine please check this page! 
    - my-funny-app.yml compose template file can be find <provide the link to the compose folder in this repo> 

8. Update the existing stack

Now it is on time to get fimilar with the rolling update capabilities of Docker Enterprise Edition. In this step we will update the stack with a image "broken" and simulate an error.


# Bonus
This demo can be extended with any known CI/CD solution, which will push all the changes automaticaly to the Docker Enterprise Edition (also known as Docker CaaS), which means either create or update the stack. In my environment I'm using a gitlab.com service combined with cirunner. For more details see .gitlab-ci.yml file inside this repo. A corresponding Docker yml file (my-funny-app.yml) can be found in the compose folder.
