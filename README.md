## Step to install locally automatic code review tool to detect bugs, vulnerabilities, and code smells in your code - [SonarQube](https://docs.sonarqube.org/latest/)

1. You can get the `docker-compose.yml` a file from this repo or get the latest version from [HERE](https://docs.sonarqube.org/latest/setup/install-server/#header-4)
2. After that run `docker-compose up` in the console from the folder where you put `docker-compose.yml` file
3. If everything is running correctly when you go [http://localhost:9000/](http://localhost:9000/) you will see SonarQube UI. If you see error maybe you have problem with Elasticsearch and you should increase `vm.max_map_count`. Please look below for a link with fixes.
4. After you are running SonarQube server you should configure your project there. After configuration SonarQube will give you parameters for running SonarScaner.
    - For login use U: admin P: admin
    - Create project <img src="https://user-images.githubusercontent.com/10156301/113424664-30bfe200-93d9-11eb-98b7-07286f44e009.png" alt="Create project" width="300">
    - Generate Token <img src="https://user-images.githubusercontent.com/10156301/113424914-9ad88700-93d9-11eb-9294-4530861a57e8.png" alt="Generate Token" width="300">
    - Use this token in point 6 <img src="https://user-images.githubusercontent.com/10156301/113424885-914f1f00-93d9-11eb-9403-2f2501e958f7.png" alt="Token" width="300">

5. Now you should create `sonar-project.properties` in folder of the project that you will scan. You can get a file from this repo or you can take a look [HERE](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/#header-1)
6. Now you should run SonarScanner to scan your code. You can take a look how to run SonarScanner from the Docker image from [HERE](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/#header-3) or you can use command below BUT NOTE YOU SHOULD CHANGE PARAMETERS WITH PARAMETERS FROM POINT 4
```
docker run --rm -e SONAR_HOST_URL="http://localhost:9000" -e SONAR_LOGIN="${TOKEN_FROM_POINT_4}" -v "${PATH_TO_YOUR_REPO}:/usr/src" sonarsource/sonar-scanner-cli -X
```
7. Go to [http://localhost:9000/](http://localhost:9000/) and see the analysis


### References & Fixes for some issues

[SonarQube Documentation](https://docs.sonarqube.org/latest/)

[Install the Server (SonarQube server)](https://docs.sonarqube.org/latest/setup/install-server/)

[SonarScanner](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)

[Elasticsearch: Max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]](https://stackoverflow.com/questions/51445846/elasticsearch-max-virtual-memory-areas-vm-max-map-count-65530-is-too-low-inc)

[ERROR: Sonar server 'http://localhost:9000' can not be reached](https://stackoverflow.com/questions/32097414/error-sonar-server-http-localhost9000-can-not-be-reached)

[scm-provider-in-sonarqube](https://stackoverflow.com/questions/28295261/how-can-i-use-git-as-the-scm-provider-in-sonarqube-5-0-using-sonar-runner)
