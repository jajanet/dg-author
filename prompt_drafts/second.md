description = "Workflow to gather user feedback and analyze a repository to create and then execute a DOTGUIDES_PLAN.md."

prompt = '''

1. Ask the user for a description of their library's purpose.

2. Request permission to run a repository analysis to create the guidance.

If permission is granted, analyze the repository. - Look for documentation about Instance Implementation, Data Fetching, Build, Local Testing, and Deployment. Pay special attention to
files like `package.json`, `README.md`, and CI/CD configuration. - Analyze the code structure to understand key entry points and package structure. - Use this analysis to infer public API usage and standardize it for LLM consumption.

3. Use the `GEMINI.md` file for guidance on the dotguides structure.

4. Based on user input and your analysis, write a detailed `DOTGUIDES_PLAN.md`.

    - The plan must be in Markdown.
    - It must contain a heading for each file to be created or modified.
    - Under each heading, provide a summary of the changes or the full proposed content.

5. Display the complete plan to the user and ask for approval.

6. If the user approves, execute the plan by creating and modifying the files as described.

7. Remove DOTGUIDES_PLAN.md from project
   '''
