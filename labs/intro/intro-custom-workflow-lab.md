# Custom Workflow Lab

## Introduction

In this lab, you will create a workflow using a starter file and customize it to trigger on specific events. You will also add steps to the workflow to interact with GitHub Actions and automate tasks.

> **Estimated Duration**: 20-30 minutes

---

## Instructions

### Step 1: Create a Custom Workflow Using the Starter File

1. Navigate to the [**Custom Workflow Starter File**](./intro-custom-workflow-starter.md).
2. Copy the content of the starter file:

   ```yaml
   name: Intro - Custom Workflow
   ```

3. In your repository, create a new workflow file under `.github/workflows` and name it `intro-custom-workflow.yml`.
4. Paste the copied content into the new file.
5. Commit the workflow file to the `main` branch.

---

### Step 2: Customize the Workflow Triggers

1. Open the `intro-custom-workflow.yml` file.
2. Add the following `on` section to define the workflow triggers:

   ```yaml
   on:
     workflow_dispatch:
     push:
       paths:
         - '.github/workflows/intro-custom-workflow.yml'
   ```

3. Commit the updated workflow to the `main` branch.
4. Trigger the workflow manually from the **Actions** tab or modify the `intro-custom-workflow.yml` file and commit the changes to see the workflow run.

---

### Step 3: Add Steps to Your Workflow

1. Open the `intro-custom-workflow.yml` file again.
2. Add the following `jobs` section to define tasks that the workflow will perform:

   ```yaml
   jobs:
     execute:
       runs-on: ubuntu-latest

       steps:
         - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
         - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
         - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."

         - name: Check Code
           uses: actions/checkout@v4

         - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
         - run: echo "🖥️ The workflow is now ready to test your code on the runner."

         - name: List Files In Directory
           run: |
             ls ${{ github.workspace }}

         - run: echo "🍏 This job's status is ${{ job.status }}."

         - name: Adding Markdown
           run: echo "### Hello world! :rocket:" >> "$GITHUB_STEP_SUMMARY"

         # This step uses GitHub's hello-world-javascript-action
         - name: Hello World
           uses: actions/hello-world-javascript-action@main
           with:
             who-to-greet: 'Mona the Octocat'
           id: hello

         # This step prints an output (time) from the previous step's action.
         - name: Echo Greeting's Time
           run: echo 'The time was ${{ steps.hello.outputs.time }}.'
   ```

3. Commit the changes to the `main` branch.
4. Trigger the workflow by modifying the file or using the **Actions** tab.

---

### Step 4: Understanding the Workflow

The `intro-custom-workflow.yml` workflow includes the following sections:

#### **Name**

The workflow is named `Intro - Custom Workflow`.

#### **Trigger (`on`)**

- **`workflow_dispatch`**:
  - Allows manual triggering of the workflow from the **Actions** tab.
- **`push`**:
  - Runs the workflow when the `.github/workflows/intro-custom-workflow.yml` file is modified and committed.

#### **Job (`jobs.execute`)**

- **`runs-on`**:

  - Specifies that the job will run on an `ubuntu-latest` GitHub-hosted runner.

- **Steps**:
  1. **Log Metadata**:
     - Outputs information about the event, runner, and repository.
  2. **Check Out Code**:
     - Uses the `actions/checkout@v4` action to clone the repository into the runner.
  3. **Run Commands**:
     - Lists the repository's files and logs the job's status.
  4. **Add Markdown Summary**:
     - Appends a message to the workflow's **Summary** tab.
  5. **Hello World Action**:
     - Greets "Mona the Octocat" using the `hello-world-javascript-action`.
  6. **Output Time**:
     - Displays the timestamp generated by the Hello World action.

---

### Step 5: Run the Workflow

1. Go to the **Actions** tab in your repository.
2. You should see the newly created workflow listed there.
3. To run the workflow:

   - If it’s triggered by a **push** event, simply make a change to the `.github/workflows/intro-custom-workflow.yml` file and commit the change.
   - Alternatively, if you want to run it manually, click the **Run workflow** button from the Actions tab and select the **main** branch.

4. The workflow will start running, and you can monitor its progress.

---

### Step 6: View the Results

1. Once the workflow has run, click on the workflow run to view its details.
2. Inside the workflow details page, click on the **run** job to view the job’s specifics.
3. Expand the step titled **Hello World** to view the output, which will include a greeting to **Mona the Octocat** and the timestamp from the action.
4. You can also review the other steps, like the repository metadata and the file listing.

---

### Optional: Trigger the Workflow on Any Push

If you want to run the workflow on any push to the repository:

1. Update the `on` section as follows:

   ```yaml
   on:
     workflow_dispatch:
     push:
       branches:
         - main
   ```

2. Commit the changes to the `main` branch.

---

## Summary

In this lab, you:

1. Created a workflow using the **Custom Workflow Starter File**.
2. Customized the workflow to trigger on specific events.
3. Added steps to perform tasks like checking out code, listing files, and greeting Mona the Octocat.
4. Ran the workflow and viewed the results.

This lab demonstrated how to create, customize, and execute a workflow using GitHub Actions.

---

## Additional Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Finding and Customizing Actions](https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions#adding-an-action-to-your-workflow)