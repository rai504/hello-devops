# Hello DevOps (CI/CD Demo)

A simple Flask web app deployed using Docker and Jenkins, with GitHub integration for automatic builds.

## Steps

1. **Run Flask App**
    ```
    pip install flask
    python app.py
    ```

2. **Dockerize**
    - Use this Dockerfile:
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

3. **Remove Old Container On Build**
    ```
    docker rm -f hello-devops 2>/dev/null || echo "Container not found or already removed."
    ```

4. **Jenkins Setup**
    - Create Freestyle job.
    - Set your GitHub repo as source.
    - Add build steps: remove old container, build image, run Docker.

5. **Auto-build on GitHub Commit**
    - In Jenkins job: enable “GitHub hook trigger for GITScm polling”.
    - In GitHub repo: Settings → Webhooks → Add webhook.
      - URL: `http://<your-jenkins-server>:8080/github-webhook/`
      - Content type: `application/json`

6. **GitHub Personal Access Token (for Jenkins)**
    - Create a token in GitHub: Profile → Settings → Developer Settings → Tokens (classic).
    - Add token to Jenkins Credentials as “Username with password”.

---

**Now every GitHub push triggers Jenkins to build and deploy your app in Docker!**

**Note:**  
If Jenkins can’t run `docker` commands because it’s missing from the default PATH, add this in the Execute Shell step:

export PATH=$PATH:/usr/local/bin

This lets Jenkins find Docker on Mac systems.

---

**Now every push to GitHub triggers Jenkins to build and deploy via Docker!**

