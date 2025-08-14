# Build Tools and Package Manager — Exercises & Solutions

**Repository to use:**  
[GitLab – build-tools-exercises](https://gitlab.com/twn-devops-bootcamp/latest/04-build-tools/build-tools-exercises)

Your task in this module is to take over an internal Java helper library project, fix issues, build it, package it, and run it with parameters.

***

## Exercise 0: Clone Project and Create Own Git Repository

**Task:**  
- Clone the provided repository.
- Remove its Git history.
- Initialize it as **your own** repository and push to your personal GitLab repo.

**Solution:**
```sh
# clone repository & change into project directory
git clone git@gitlab.com:twn-devops-bootcamp/latest/04-build-tools/build-tools-exercises.git
cd build-tools-exercises

# remove old Git history & initialize your own repo
rm -rf .git
git init
git add .
git commit -m "initial commit"

# add your remote GitLab repository & push
git remote add origin git@gitlab.com:{gitlab-user}/{gitlab-repo}.git
git push -u origin master
```

***

## Exercise 1: Build JAR Artifact

**Task:**  
- Try to build the JAR file using Gradle.  
- You will get a compile error due to a failing test.

**Solution:**
```sh
gradle build
```
**Note:** The build fails here because of a broken test — you’ll fix this in Exercise 2.

***

## Exercise 2: Run Tests

**Task:**  
- Fix the failing test in `AppTest.java`.  
- Change `"true"` (string) to `true` (boolean) on **line 22**.  
- Run only the tests to confirm the fix.

**Solution:**
```java
// In src/test/java/.../AppTest.java
boolean result = myApp.getCondition(true);
```

```sh
# run tests
gradle test
```

***

## Exercise 3: Clean & Build App

**Task:**  
- Clean the build folder.  
- Rebuild the JAR file after fixing the test.

**Solution:**
```sh
gradle clean
gradle build
```

***

## Exercise 4: Start Application

**Task:**  
- Start the packaged application to ensure it runs successfully as a JAR.  
- The JAR will be found in `build/libs`.

**Solution:**
```sh
java -jar bootcamp-java-project-1.0-SNAPSHOT.jar
```
*(Adjust filename if your JAR version/name differs.)*

***

## Exercise 5: Start App with 2 Parameters

**Task:**  
- Modify `Application.java` to accept **two parameters** at startup and log them.  
- Rebuild the project.  
- Run the JAR with two arguments of your choice.

**Solution:**  
*In `Application.java` at **line 16**, add:*
```java
Logger log = LoggerFactory.getLogger(Application.class);
try {
    String one = args[0];
    String two = args[1];
    log.info("Application will start with the parameters {} and {}", one, two);
} catch (Exception e) {
    log.info("No parameters provided");
}
```

**Rebuild and Run:**
```sh
gradle build
java -jar bootcamp-java-project-1.0-SNAPSHOT.jar myname mylastname
```
