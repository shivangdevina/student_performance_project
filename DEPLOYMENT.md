# AWS Elastic Beanstalk Deployment Guide

This guide will walk you through deploying your `student_performance_project` to AWS Elastic Beanstalk using GitHub Actions.

---

## 1. Create the AWS Elastic Beanstalk Environment

First, you need to create the application to which GitHub will deploy.

1.  **Log in to AWS Console** and search for **Elastic Beanstalk**.
2.  Click **Create Application**.
3.  **Application Name**: `student_performance`
    - *(If you choose a different name, update line 24 in `.github/workflows/deploy.yml`)*
4.  **Platform**: select **Python** (Python 3.8 or 3.9 recommended).
5.  **Application Code**: select **Sample application** for now.
6.  Click **Configure more options** (optional, to verify settings) or just click **Create Application**.
7.  Wait for the environment to launch. It will be named something like `Studentperformance-env`.
    - *(If the name is different, update line 25 in `.github/workflows/deploy.yml`)*

## 2. Configure GitHub Secrets

GitHub needs permission to deploy to your AWS account. You must add your AWS credentials as secrets.

1.  Go to your GitHub Repository page.
2.  Click on **Settings** > **Secrets and variables** > **Actions**.
3.  Click **New repository secret**.
4.  Add the following secrets:
    - **Name**: `AWS_ACCESS_KEY_ID`
      - **Value**: Your AWS Access Key ID (starts with AKIA...)
    - **Name**: `AWS_SECRET_ACCESS_KEY`
      - **Value**: Your AWS Secret Access Key (starts with different characters)

> **Note**: If you don't have access keys, go to **AWS IAM** > **Users** > Select your user > **Security credentials** > **Create access key**.

## 3. Trigger Deployment

The deployment is automated. Any push to the `main` branch will start the process.

1.  Open your terminal in the project folder.
2.  Commit your changes:
    ```bash
    git add .
    git commit -m "Configure deployment for AWS Elastic Beanstalk"
    ```
3.  Push to GitHub:
    ```bash
    git push origin main
    ```

## 4. Monitor Deployment

1.  In your GitHub Repository, click the **Actions** tab.
2.  You should see a workflow running named "Deploy to AWS Elastic Beanstalk".
3.  Click on it to watch the steps (Build, Deploy).
4.  Once it turns green (Success), go back to the AWS Elastic Beanstalk Console.
5.  Click the URL under your environment name (e.g., `http://Studentperformance-env.eba-xxxxxx.us-east-1.elasticbeanstalk.com`).
6.  Your application should be live!

## troubleshooting

-   **Deployment Fails**: Check the "Deploy to EB" step logs in GitHub Actions.
-   **App Crashes (502 Bad Gateway)**:
    -   Go to your Elastic Beanstalk Environment.
    -   Click **Logs** on the left menu.
    -   Request **Last 100 Lines**.
    -   Look for errors in `web.stdout.log` or `eb-engine.log`.
