---
sidebar_position: 1
---

# Tutorial Intro

Let's discover **TireWizards in less than 5 minutes**.

## Tire Wizard Retail Site Application

### What you'll need

- [Node.js](https://nodejs.org/en/download/) version 16.14 or above:
  - When installing Node.js, you are recommended to check all checkboxes related to dependencies.

## Start your site | Development Server Setup

This documentation will guide you through the process of setting up and running your development server. We will utilize two terminal commands to perform this task.

1. Open your terminal or command prompt
2. Navigate to the directory where you want to create your project

  ```bash
  cd repo-name 
  ```

:::info Important Note
Replace 'repo-name' with the actual name of your repository.
:::

1. Run the backend server with the following command:

```bash
npm run start
```

### Frontend Server Setup

1. Open a new terminal window. This should run parallel with the terminal where your backend server is operating.

2. Navigate to the project repository, similar to how we did in the backend server:

```bash
cd repo-name
```

:::info Important Note
Again, replace 'repo-name' with the actual name of your repository.

:::
1. Run the frontend server with the following command:


```bash
gulp 

```

The `cd` command changes the directory you're working with. In order to work with your newly created Docusaurus site, you'll need to navigate the terminal there.

The `npm run start` command runs your backend server

The `gulp` command runs your frontend server - this will run on port 3000

:::danger Important Note
Please be aware that your frontend server will not run if you have not executed the **gulp** command. Therefore, it's crucial to remember to start both the backend and frontend servers when developing and testing your application.

By following these steps, you will have successfully set up and initiated both your backend and frontend servers, and you should now be ready to proceed with development.

:::

#### Reference Links (Dealer Site)

- QA Environment : [https://app.qa-tirelocator.space/testwizarddealer](https://app.qa-tirelocator.space/testwizarddealer)
- Stage Environment : [https://app.stage-tirelocator.space/testwizarddealer](https://tire-wizard-stage.herokuapp.com/testwizarddealer)
- Production Environment : [https://app.tirelocator.ca/testwizarddealer](https://app.tirelocator.ca/testwizarddealer)

#### Reference Links (National Site)

- QA Environment : [https://app.qa-tirelocator.space/national/testwizard](https://app.qa-tirelocator.space/national/testwizard)
- Stage Environment : [https://app.stage-tirelocator.space/national/testwizard](https://app.stage-tirelocator.space/national/testwizard)
- Production Environment : [https://app.tirelocator.ca/national/testwizard](https://app.tirelocator.ca/national/testwizard)
