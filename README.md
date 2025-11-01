# DevOps-EXP7 Sample Maven Project

A tiny Java + Maven project designed for Jenkins **Problem Statement C**:

- Configure Maven as a global tool
- Create build & test stages
- Convert to **Pipeline as Code** (Scripted & Declarative)
- Include a `Jenkinsfile`

## Project Structure
```
DevOps-EXP7/
├─ Jenkinsfile
├─ Jenkinsfile.scripted
├─ pom.xml
├─ src/
│  ├─ main/java/com/example/app/App.java
│  └─ test/java/com/example/app/AppTest.java
└─ .gitignore
```

## Build locally
```bash
mvn -B -DskipTests=true clean package
mvn -B test
```

The artifact will be at `target/devops-exp7-1.0.0.jar`.

## Jenkins notes

### Tools (Manage Jenkins → Tools)
- JDK: **JDK17**
- Maven: **M3**

### Job Types
- **Declarative pipeline job** → points to `Jenkinsfile`
- **Scripted pipeline job** → points to `Jenkinsfile.scripted`

Both Jenkinsfiles include:
- Checkout
- Build (`clean package`, tests skipped)
- Test (`mvn test` + JUnit publishing)
- Archive artifacts (`target/*.jar`)

> If you run classic Freestyle jobs first (for learning), use:
> - Build: `-B -DskipTests=true clean package`
> - Test: `-B test` and publish `target/surefire-reports/*.xml`

## How to push to GitHub (once you create an empty repo)

```bash
git init
git add .
git commit -m "Initial commit: DevOps-EXP7 sample with Jenkinsfiles"
git branch -M main
git remote add origin https://github.com/<your-username>/DevOps-EXP7.git
git push -u origin main
```