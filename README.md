# Sonarqube-Scanner
Docker Image for Sonarqube-Scanner CLI

# Supported tags and respective `Dockerfile` links

-	[`3.2.0`, `3.2.0.1227`, `latest` (*Dockerfile*)](https://github.com/ElectroStar/Sonar-Scanner/blob/100820802d091ac3d8bed4cff9c63bdcddbba516/Dockerfile)
-	[`3.1.0`, `3.1.0.1141` (*Dockerfile*)](https://github.com/ElectroStar/Sonar-Scanner/blob/41e32ad2a0a7cae298fd795b3dd365a5aee37cb5/Dockerfile)
-	[`3.0.3`, `3.0.3.778` (*Dockerfile*)](https://github.com/ElectroStar/Sonar-Scanner/blob/4200455bdb40a128ec0a841bcf8fbfb6ead2e498/Dockerfile)
-	[`3.0.2`, `3.0.2.768` (*Dockerfile*)](https://github.com/ElectroStar/Sonar-Scanner/blob/da9f881a95aeaf7b5a3bb34b9e3756eaf8599a17/Dockerfile)
-	[`3.0.1`, `3.0.1.733` (*Dockerfile*)](https://github.com/ElectroStar/Sonar-Scanner/blob/2ca5796c91a6e6439cfd2deb461d960552f7a0db/Dockerfile)
-	[`3.0.0`, `3.0.0.702` (*Dockerfile*)](https://github.com/ElectroStar/Sonar-Scanner/blob/ed2886c7dd97348854065b93ab6b65a7715c00a4/Dockerfile)
-	[`2.9.0`, `2.9.0.670` (*Dockerfile*)](https://github.com/ElectroStar/Sonar-Scanner/blob/00f57d4103db35e21936ffc4c198c6be3265ce8d/Dockerfile)
-	[`2.8` (*Dockerfile*)](https://github.com/ElectroStar/Sonar-Scanner/blob/5b5913f732f1b6018f01f1b0f669068193689fe1/Dockerfile)

# Quick reference

-	**Where to get help**:  
  [the Docker Community Forums](https://forums.docker.com/), [the Docker Community Slack](https://blog.docker.com/2016/11/introducing-docker-community-directory-docker-community-slack/), or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)

-	**Where to file issues**:  
	[GitHub Issues Page](https://github.com/ElectroStar/Sonar-Scanner/issues)

-	**Maintained by**:  
	[ElectroStar](https://github.com/ElectroStar)

### How to use this Image

To use this Image with Gitlab-CI for Sonarqube Codechecking with installed [Gitlab-Plugin](https://gitlab.talanlabs.com/gabriel-allaigre/sonar-gitlab-plugin) for reporting, use the following commands in a .gitlab-ci.yml - File:


```
variables:
  SONAR_URL: "http://YOUR-SONAR-Server/"
  
stages:
  - test

sonarqube_preview:
  stage: test
  image: electrostar/sonar-scanner:latest
  script:
    - git checkout origin/master
    - git merge $CI_COMMIT_SHA --no-commit --no-ff
    - sonar-scanner -Dsonar.host.url=$SONAR_URL -Dsonar.sources="." -Dsonar.projectKey="${CI_PROJECT_NAME}_${CI_PROJECT_ID}" -Dsonar.projectName="$CI_PROJECT_NAME" -Dsonar.analysis.mode=preview -Dsonar.gitlab.project_id=$CI_PROJECT_PATH -Dsonar.gitlab.commit_sha=$CI_COMMIT_SHA -Dsonar.gitlab.ref_name=$CI_COMMIT_REF_NAME  -Dsonar.projectDescription="$CI_PROJECT_NAMESPACE"
  except:
    - develop
    - master
    - /^hotfix_.*$/
    - /.*-hotfix$/

sonarqube:
  stage: test
  image: electrostar/sonar-scanner:latest
  script:
  - sonar-scanner -Dsonar.host.url=$SONAR_URL -Dsonar.sources="." -Dsonar.projectKey="${CI_PROJECT_NAME}_${CI_PROJECT_ID}" -Dsonar.projectName="$CI_PROJECT_NAME" -Dsonar.projectDescription="$CI_PROJECT_NAMESPACE"
  only:
    - master
```
Just replace YOUR-SONAR-SERVER with the IP-Address of your Sonar-Server of your choice.

# License

The Dockerfiles and associated scripts are licensed under the [MIT License](https://github.com/ElectroStar/Sonar-Scanner/blob/master/LICENSE).
