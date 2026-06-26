
# Jenkins HTML Demo

A simple HTML project integrated with Jenkins Pipeline. This project demonstrates how Jenkins pulls source code from a GitHub repository and executes a pipeline automatically.

---

##  Project Structure

```

jenkins-html-demo/
│── Jenkinsfile
│── index.html
└── README.md

````

---

##  Technologies Used

- HTML5
- CSS (Inline)
- Git
- GitHub
- Jenkins Pipeline

---

##  Prerequisites

- Git installed
- Jenkins installed and running
- GitHub account
- Pipeline Plugin installed in Jenkins

---

##  Workflow

1. Create a GitHub repository.
2. Add `index.html`, `Jenkinsfile`, and `README.md`.
3. Push the code to GitHub.
4. Create a Jenkins Pipeline job.
5. Connect the Pipeline job to the GitHub repository.
6. Run the pipeline manually or trigger it automatically using GitHub Webhooks.
7. Jenkins clones the repository and executes the pipeline.

---

##  Pipeline Stages

- Clone GitHub Repository
- List Workspace Files
- Display HTML File
- Archive Build Artifacts (Optional)

---

## Clone Repository

```bash
git clone https://github.com/<your-username>/jenkins-html-demo.git
````

Move into the project directory:

```bash
cd jenkins-html-demo
```

---

##  Push Changes

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

---

##  Jenkinsfile

The Jenkins Pipeline performs the following tasks:

* Pulls the latest code from GitHub
* Lists the project files
* Displays the contents of `index.html`
* Archives build artifacts (optional)

---

##  Learning Objectives

* Create a GitHub repository
* Clone a repository using Git
* Configure a Jenkins Pipeline
* Integrate Jenkins with GitHub
* Automate builds using GitHub Webhooks

---

## Author

**Neha**


