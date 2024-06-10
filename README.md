# Complete Guide to Creating and Pushing Docker Images to Amazon ECR

# step 1:- first we need docker on top of ubuntu system

# Install using the apt repository

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

1: Set up Docker's apt repository

#Add Docker's official GPG key:

$sudo apt-get update

$sudo apt-get install ca-certificates curl

$sudo install -m 0755 -d /etc/apt/keyrings

$sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

$sudo chmod a+r /etc/apt/keyrings/docker.asc

#Add the repository to Apt sources:

$echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
$sudo apt-get update

![Screenshot (383)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/74b25148-89cd-4c16-bd0d-3040a005ffb1)

2: To install the latest version, run:

$sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
![Screenshot (384)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/9f79d6b0-684f-4713-a2c8-276a9a65cf1b)


3: Verify that the Docker Engine installation is successful by running the hello-world image.

$sudo docker run hello-world
![Screenshot (385)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/c80226fc-948c-4888-a427-f9db48371efb)

then check the status of docker $systemctl status docker
![Screenshot (386)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/e4d57470-3825-48eb-be45-734af5c790e0)

# step2 :- install AWS CLI on my machine
![Screenshot (387)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/75fe3597-44b0-404c-89ac-00035215b8ae)

# Step3 :- Create an IAM User
In AWS management console, Go to IAM service, create an IAM user
![Screenshot (388)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/ee3fdb75-9e47-4181-b714-5ed5942d4237)

Attach policies to the user
![Screenshot (389)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/81207f19-4914-411e-beab-a7a21029e2cd)

User is created successfully.
![Screenshot (390)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/de6b7a0b-7dc9-4cbc-9b68-25c6ed35d654)

Go to security credentials
![Screenshot (391)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/52591fda-eaf8-4a39-a9a6-7aea96136f4f)

Click on create access key
![Screenshot (392)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/2496ee30-0059-4272-993f-a13752ed83a6)
![Screenshot (393)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/ffb05830-b97a-4b52-92e0-b34bd414c0e6)

Download .csv file which contain access key and secret access key
![Screenshot (394)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/bf808db7-c5ae-43e4-9721-2faa629311e3)

Step 4: Configure AWS CLI
Enter AWS access key, secret access key , default region and default output format.
![Screenshot (395)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/0c928001-df12-40ba-a43f-1e064f7d1ef3)

Step 5: Create an ECR Repository
You can create Repository using AWS management console or AWS cli.

Run the following command to create a new ECR repository using AWS cli. Replace repository-name with your desired repository name.

aws ecr create-repository --repository-name your-repository-name
![Screenshot (396)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/741dcfc0-ee70-43ed-ac8c-a2d5b121d2a4)

In the Amazon ECR console, select “Repositories” from the left navigation pane.

Click the “Create repository” button.
![Screenshot (397)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/fb02d296-7a46-4ff8-9e54-4ef1a2accdb6)

Enter a unique name for your repository in the “Repository name” field.
![Screenshot (398)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/40bb4f6e-e954-4a79-8156-dd675a8f0a27)

Repository is created
![Screenshot (399)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/0622047b-7a60-41f2-bb1b-6768ef091683)

Step 6: Build Docker Image Locally
Using your machine, navigate to the directory containing your Dockerfile
![Screenshot (404)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/7aeedb87-37bc-48aa-9557-b116822da74d)

Build Docker image, with build command

& check the image with $docker images
![Screenshot (403)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/a976cc3f-90ed-4bdc-af39-b8157b22af3b)

Step 7: Push Docker Image to ECR
1. Go back to the AWS Management Console.

2. In the Amazon ECR console, select your repository from the list.

3. In the repository details, click the “View push commands” button.
![Screenshot (405)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/29ef2624-2ae0-4e38-8787-a5b6fdda0d05)

4. Follow the provided instructions to authenticate Docker with your ECR registry and push your Docker image.
![Screenshot (406)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/ef022e35-db38-4a20-939f-275b73de8195)

1 Retrieve an authentication token and authenticate your Docker client to your registry. Use the AWS CLI:
aws ecr get-login-password — region ap-south-1 | docker login — username AWS — password-stdin 905418112275.dkr.ecr.ap-south-1.amazonaws.com
![Screenshot (407)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/3b27744f-b630-4b8b-89ff-39629a99bb32)

2. Build your Docker image using the docker build command. You can skip this step if your image is already built.

3. After the build completes, tag your image so you can push the image to this repository:

docker tag uma:latest 905418112275.dkr.ecr.ap-south-1.amazonaws.com/uma:latest
![Screenshot (408)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/e4d80075-e746-40b5-9ace-53f1dc68ba51)

4. Run the following command to push this image to your newly created AWS repository:

docker push 905418112275.dkr.ecr.ap-south-1.amazonaws.com/uma:latest
![Screenshot (409)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/c82cd0e6-2e1e-4fc7-973e-48821156380c)

Step 7: Verify Image in ECR Console
Once the image is pushed, go back to the Amazon ECR console. Select your repository.

Check the “Images” tab to verify that your Docker image has been successfully pushed.
![Screenshot (410)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/d823a46a-8008-4fc2-a003-21e3545cbed7)
![Screenshot (411)](https://github.com/manikantaraju427/Complete-Guide-to-Creating-and-Pushing-Docker-Images-to-Amazon-ECR/assets/125948783/6b54f33e-f498-492b-aa7b-d8df474344ff)

image is successfully pushed into AWS ECR





