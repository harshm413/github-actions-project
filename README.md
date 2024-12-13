## CI/CD Pipeline for Vite React Project

This repository is set up with a complete Continuous Integration and Continuous Deployment (CI/CD) pipeline using GitHub Actions. The pipeline performs the following tasks:

- **Build Project**: Installs dependencies and builds the Vite React project.
- **Run Tests**: Executes tests after the build process.
- **Deploy**: Deploys the application to different environments (development, staging, production).

## CI/CD Workflow Overview

The workflow is triggered on several events:

1. **Push to main or tagged version**: The pipeline triggers when changes are pushed to the `main` branch or any version tag starting with `v*`.
2. **Pull Request**: The pipeline also runs for pull requests to the `main` branch.
3. **Scheduled Cron Job**: It runs daily at midnight UTC.
4. **Manual Trigger (Workflow Dispatch)**: The pipeline can be triggered manually with options to select the deployment environment (development, staging, production) and provide a version number.

## Jobs and Steps

### 1. **Build Job**

#### **Step 1: Checkout Code**

**Logs Output:**
```
<No output from this step as it is the checkout process>
```

#### **Step 2: Install Dependencies**

**Logs Output:**
```
Installing dependencies...
GLOBAL_VAR=GlobalEnvironmentVariableValue
BUILD_ENV=BuildJobEnvironmentValue

added 255 packages, and audited 256 packages in 12s

106 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

#### **Step 3: Build Project**

**Logs Output:**
```
Building Vite React project...
NODE_ENV=production

> github-actions-project@0.0.0 build
> vite build

vite v6.0.3 building for production...
transforming...
✓ 30 modules transformed.
rendering chunks...
computing gzip size...
dist/index.html                   0.46 kB │ gzip:  0.29 kB
dist/assets/react-CHdo91hT.svg    4.13 kB │ gzip:  2.05 kB
dist/assets/index-n_ryQ3BS.css    1.39 kB │ gzip:  0.71 kB
dist/assets/index-uO412iEj.js   143.90 kB │ gzip: 46.34 kB
✓ built in 847ms
```

#### **Step 4: Save Build Output**

**Logs Output:**
```
build_status=success
Custom Input Provided: custom-build-value
```

#### **Step 5: Upload Artifacts**

**Logs Output:**
```
<No output provided for uploading artifacts, as it is a file upload process>
```

### 2. **Test Job**

This job depends on the success of the **Build Job**.

#### **Step 1: Checkout Code**

**Logs Output:**
```
<No output from this step as it is the checkout process>
```

#### **Step 2: Run Tests**

**Logs Output:**
```
Running tests...
TEST_ENV=TestJobEnvironmentValue
GLOBAL_VAR=GlobalEnvironmentVariableValue
Build Output: success
Test Param Provided: test-param-value
```

#### **Step 3: Save Test Output**

**Logs Output:**
```
test_status=passed
```

#### **Step 4: Download Artifacts**

**Logs Output:**
```
<No output from this step as it is the artifact download process>
```

#### **Step 5: Output Artifacts Content**

**Logs Output:**
```
assets
index.html
vite.svg
```

### 3. **Deploy Job**

This job depends on the success of both the **Build Job** and **Test Job**.

#### **Step 1: Deploy to Environment**

**Logs Output:**
```
Deploying Vite React application...
DEPLOY_ENV=DeploymentJobEnvironmentValue
GLOBAL_VAR=GlobalEnvironmentVariableValue
Test Output: passed
```

#### **Step 2: Download Artifacts**

**Logs Output:**
```
<No output from this step as it is the artifact download process>
```

#### **Step 3: Output Artifacts Content**

**Logs Output:**
```
assets
index.html
vite.svg
```

#### **Step 4: Save Deployment Output**

**Logs Output:**
```
deployment_status=success
```

## Environment Variables

The following environment variables are used in the workflow:

- `GLOBAL_VAR`: A global variable used across all jobs in the pipeline.
- `BUILD_ENV`: Specifies the environment for the build process.
- `TEST_ENV`: Specifies the environment for the testing process.
- `DEPLOY_ENV`: Specifies the deployment environment.
- `NODE_ENV`: Set to `production` during the build phase.
  
## Usage

### Triggering the Workflow

- **Push**: Automatically triggered when code is pushed to the `main` branch or a tag is created (e.g., `v1.0`).
- **Pull Request**: Automatically triggered when a pull request is made to the `main` branch.
- **Scheduled Cron Job**: The workflow runs daily at midnight UTC.
- **Manual Trigger**: You can manually trigger the workflow via the GitHub Actions interface, allowing you to specify the deployment environment and version.

### Example Workflow Dispatch Input

When manually triggered, the following inputs are provided:

- **environment**: Choose the deployment environment (`development`, `staging`, `production`).
- **version**: Specify the version number to deploy.
