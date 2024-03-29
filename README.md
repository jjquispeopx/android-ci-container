# android-ci-container

This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool like GitLab CI. Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs.

A `.gitlab-ci.yml` with caching of your project's dependencies would look like this:

```
image: jjquispeopx/android-ci-container:<tag>

stages:
  - build

before_script:
  - export GRADLE_USER_HOME=$(pwd)/.gradle
  - chmod +x ./gradlew

cache:
  key: ${CI_PROJECT_ID}
  paths:
    - .gradle/

build:
  stage: build
  script:
    - ./gradlew assembleDebug
  artifacts:
    paths:
      - </path_of_the_apk_build>/app-debug.apk
```

# Inspired by

- [gitlab-ci-android](https://github.com/jangrewe/gitlab-ci-android)
- [docker-android-build-box](https://github.com/jangrewe/gitlab-ci-android)
