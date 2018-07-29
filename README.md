# jonbulica/android-ci-ndk

### Continous Integration (CI) for Android apps on GitLab
An image for building Android apps with support for multiple SDK Build Tools. 
This Docker image contains the Android SDK, the NDK and the most common packages 
necessary for building Android apps in a CI tool. Based on 
[javiersantos/android-ci](https://github.com/javiersantos/android-ci).

You can define additional packages by adding them to the `packages.txt` file.

## Sample Implementation
### GitLab (`.gitlab-ci.yml`)
```yml
image: jonbulica/android-ci-ndk:latest

before_script:
    - export GRADLE_USER_HOME=`pwd`/.gradle
    - chmod +x ./gradlew

cache:
  key: "$CI_COMMIT_REF_NAME"
  paths:
     - .gradle/

stages:
  - build

build:
  stage: build
  script:
     - ./gradlew assembleDebug
  artifacts:
    paths:
      - app/build/outputs/apk/
```
