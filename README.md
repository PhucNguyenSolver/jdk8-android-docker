## Build Android app with Docker
We will use the Docker image from: `phucsolver/jdk8-android`

### Build commands
```
step 'Inject SDK location':
    echo "sdk.dir=$ANDROID_HOME" > local.properties

step 'Build apk':
    ./gradlew clean
    ./gradlew assembleDevDebug

artifacts:
    app/build/outputs/apk/dev/debug/

```

### Run Docker locally for debugging
Note: On Linux/Unix machine, we need to use $(PWD) instead of %cd%
```
step 'Run docker in interactive mode':    
    docker run -it ^
    --volume=%cd%:/opt/workspace ^
    --workdir=/opt/workspace ^
    --rm phucsolver/jdk8-android ^
    /bin/bash    
```

### Common issues
Bitbucket cần check đúng branch của submodule
    branch=18_07_2022
	Trong ErrorUtil.kt: response.body -> response.body()
- Trong gradlew: sửa line ending CRLF -> LF


### Useful command:
```
describe 'Docker: Exec into running container':
    docker exec -it /bin/bash

describe 'Gradle: check version':
    ./gradlew --version

describe 'Gradle: list all tasks':
    ./gradlew tasks --all
```