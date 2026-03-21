* ##### Run JMeter test in docker container

  1. Download and install docker desktop in you local machine (https://www.docker.com/products/docker-desktop/)
  2. Download JMeter image using the command in command prompt. (Command : docker pull justb4/jmeter)
  3. To see all available/downloaded images in your docker desktop use this command : docker images
  4. Run the Jmeter in the docker container using this command : docker run justb4/jmeter
  5. Run the actual jmeter test in docker container use this command : docker run --rm -v  C:\\Users\\prasa\\Downloads\\apache-jmeter-5.6.3\\apache-jmeter-5.6.3\\bin\\examples:/test justb4/jmeter -n -t /test/CSVSample.jmx -l /test/results1.jtl

     * docker run = it starts the docker container
     * \--rm = destroy/delete docker container once execution is completed
     * \-v  C:\\Users\\prasa\\Downloads\\apache-jmeter-5.6.3\\apache-jmeter-5.6.3\\bin\\examples:/test = mounts your local jmeter script folder into container
     * justb4/jmeter = this will start jmeter and its dependencies present in this image in the container
     * \-n -t /test/CSVSample.jmx = run the jmeter jmeter test plan in non gui mode
     * \-l /test/results1.jtl = store the results in the .jtl file
* ##### Run JMeter test with GitHub action using its own runner(VM)

  1. Install git in your local machine (https://git-scm.com/install/windows)
  2. Login to GitHub and create repository to GitHub
  3. Follow below command to setup the repo and upload file to GitHub (Create Folder in your local machine and open gitbash for the folder)

     * git init = initializes new git repo in your project folder
     * Add file in your folder and then use this command to upload file to repo = git add <file name>
     * then commit changes to the repository it will upload the file successfully to repo = git commit -m "give message here"
     * git add remote origin <add repo URL> = this is used so that we can push and pull file to repo from local and remote
     * git push = changes will pushed to repository
  4. Now you have JMX and CSV files to your repository. Now create GitHub action workflow. Actions > New workflow > Set up a workflow yourself > write yml code and click on commit changes
  5. Again go to actions > go to your workflow > run workflow (if you want to force start it)
  6. Results file will be stored in repo
* ##### Run JMeter test using GitHub action using docker container (self hosted runner)

  1. Create GitHub action workflow. Actions > New workflow > Set up a workflow yourself > write yml code and click on commit changes
  2. Create runner on GitHub = Actions > Runners > New runner > new self hosted runner > Follow the steps given in the page
  3. To start the runner when needed to execute the test use this command : Got to runner folder (C:\\Users\\prasa\\actions-runner) > run.cmd (runner will connect to GitHub)
  4. Suppose you don't want to start repeatedly when required then you can install it as background service = .\\svc install > .\\svc start (now your runner will keep running and will always listen to GitHub for any job)
  5. you will get below errors **running scripts is disabled on this system PSSecurityException**
  6. open windows PowerShell as administrator and use this command : Set-ExecutionPolicy -Scope LocalMachine -ExecutionPolicy RemoteSigned > say Yes
  7. Once execution is done you can again reset policy back for that use this command : Set-ExecutionPolicy -Scope LocalMachine -ExecutionPolicy Restricted > say Yes
  8. Now follow this process to start the workflow : actions > go to your workflow > run workflow (if you want to force start it)
  9. Results file will be stored in action runner folder in your local machine

