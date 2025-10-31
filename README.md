Here’s a concise README.md with your extra note for **Jenkins running locally on Mac**:

***

```markdown
# Hello DevOps (CI/CD Demo)

A simple Flask app deployed using Docker and Jenkins with auto-builds from GitHub commits.

## Steps

1. **Run Flask App**
    ```
    pip install flask
    python app.py
    ```

2. **Dockerize**
    - Dockerfile:
      ```
      FROM python:3.10-slim
      WORKDIR /app
      COPY app.py .
      RUN pip install flask
      CMD ["python", "app.py"]
      ```
    - Build & run:
      ```
      docker build -t hello-devops .
      docker run -d --name hello-devops -p 5000:5000 hello-devops
      ```

3. **Remove Old Container Before Build**
    ```
    docker rm -f hello-devops 2>/dev/null || echo "Container not found or already removed."
    ```

4. **Jenkins Setup**
    - Freestyle job with your repo as source.
    - Build steps: (add before any docker commands)
      ```
      export PATH=$PATH:/usr/local/bin
      docker rm -f hello-devops 2>/dev/null || echo "Container not found or already removed."
      docker build -t hello-devops .
      docker run -d --name hello-devops -p 5000:5000 hello-devops
      ```

5. **Auto-build on GitHub Commits**
    - Enable “GitHub hook trigger for GITScm polling” in Jenkins.
    - Add a webhook in your GitHub repo:
      - URL: `http://<your-jenkins-server>:8080/github-webhook/`
      - Content type: `application/json`

6. **GitHub Personal Access Token**
    - Create a token via GitHub settings.
    - Add to Jenkins Credentials as “Username with password”.

---

**Note:**  
If Jenkins can’t run `docker` commands because it’s missing from the default PATH, add this in the Execute Shell step:
```
export PATH=$PATH:/usr/local/bin
```
This lets Jenkins find Docker on Mac systems.

---

**Now every push to GitHub triggers Jenkins to build and deploy via Docker!**
```

***

Let me know if you want more tweaks or explanations!
