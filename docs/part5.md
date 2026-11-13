
# Context engineering and agent AI

**by Professor Andrew Garrard MEng(hons) PhD CEng FIMechE PFHEA** 

## Learning Outcomes
- Explain the difference between agentic and chat window based use of AI
- Explain how AI can be used to undertake engineering tasks, including the opportunities and limitations of autonomous operation.
- Identify opportunities to use AI to improve the effectiveness and efficiency of engineering workflows.
- Apply appropriate approaches to configuring and using AI tools to undertake practical engineering tasks.
- Evaluate the effectiveness, reliability and risks of AI-assisted workflows, including the appropriate level of human oversight.

## AI Agents

An AI agent uses an AI model to undertake tasks autonomously, including interacting with its environment and taking actions on behalf of a user.  Unlike using AI through a chat interface, where the outcome is typically information presented to the user, an AI agent can take actions such as modifying files, interacting with the internet or executing terminal commands. Agents are not necessarily more intelligent than equivalent models accessed through a chat interface. Their advantage is that they can interact with their environment and act upon the results.

To use an AI agent effectively as an engineer, a useful approach is to retain responsibility for high-level decisions about the implementation strategy and delegate more routine or administrative tasks to the agent.


### Examples of how agentic AI differs from using an AI chat interface

<div class="admonition example">
  <p class="admonition-title">Example</p>
  <p>For example, a chat interface could be prompted to write Python code to rename files in a directory (called a folder in Windows). The code would then need to be copied from the chat interface and executed on a computer. Alternatively, a similar prompt could be provided to an AI agent. The agent could autonomously examine the files in the directory, generate the necessary code and execute it on the computer.

  Another example would be creating a web application running on a Raspberry Pi to control a connected LED based on sensor data. As with the previous example, a chat interface could generate the code and provide instructions for installing, deploying and validating the application. Alternatively, an AI agent with the necessary access could interact directly with the Raspberry Pi's operating system, download and install the required software (for example, a web server and the necessary libraries for interacting with the Raspberry Pi's GPIO pins), generate and execute code, deploy the application and perform tests to check that it operates as intended, provided it has suitable access to feedback from the connected hardware.</p>
</div>


## Using agents safely

Agentic AI is an extremely powerful tool that can be used to undertake complex or long-running tasks with minimal manual input. Complex systems consisting of multiple files and thousands of lines of code can be created with relatively little human input beyond specifying the desired requirements. However, the resulting systems still require appropriate testing and validation to establish that they meet those requirements. Even when the stated requirements are met, the outcome may not fully reflect the user's original vision, making further refinement necessary. Nevertheless, AI capabilities in this area are developing rapidly.

This capability also carries risks. It is important to ensure that an agent's access to files and systems is limited to what is necessary to complete the tasks it has been assigned. This can be achieved through sandboxing, the use of virtual machines and appropriate access permissions. Agentic tools also typically provide different levels of autonomy, such as:

- Suggest actions for me to perform manually.
- Request my approval before taking actions.
- Take actions without requesting approval.

As users gain experience with an AI agent, their confidence in its ability to perform particular tasks may increase, leading them to grant it greater autonomy. Repeatedly authorising actions that are consistently sensible and aligned with the objectives of the task can become frustrating, creating an incentive to allow the agent to operate with less supervision. However, this trust should be based on verification that the agent's actions are appropriate and produce the intended results, rather than simply on the apparent success of previous tasks.

## A harness

An AI agent requires a *harness*. A harness is software that manages communication with an AI model (such as Gemini, GPT or Claude) and enables the model to interact with its environment and execute tasks. The harness sends information and instructions to the model as input tokens, receives its responses as output tokens and translates requests for actions into operations on the computer or other connected systems.

An example of a harness is an AI agent extension for Visual Studio Code (VS Code). VS Code is a development environment that allows users to open, create and edit files on a local or remote computer. By installing an agent extension and connecting it to an AI model, either through a subscription or an API, the model can be used to perform agentic tasks such as modifying files, executing commands and testing code.

For an agent to undertake complex tasks requiring an extended sequence of actions (sometimes called *long-horizon tasks*), the concept of **context** is particularly important. Context can refer to two different but related concepts:
- Context for the task
- The model's context window

## Context

The context for a task is the information an agent needs to achieve the desired outcome. For example, if an agent were asked to develop a tool for managing project budgets, it would benefit from a detailed description of the required functionality and how users should interact with it. Access to previous accounts and transactions would provide further context, enabling the agent to develop a more suitable application.

When working with an agent, it is not always necessary to explicitly provide all the context through the harness. Instead, an agent can be given access to a directory containing relevant files, from which it can retrieve information as required. This differs from a conventional chat interface, where relevant files and information generally need to be supplied directly by the user.

Context can take several forms. Three useful categories of contextual information are:

- Existing information. Information that is already available and relevant to the task, such as example data, policy documents, technical specifications or software documentation.
- Persistent instructions. Instructions that guide how an agent should operate, including preferred working practices, constraints and high-level objectives. These instructions can be retained and applied consistently across multiple tasks or sessions.
- Records of previous work. Documentation of work already undertaken, including design decisions, their rationale, established conventions and progress towards the intended outcome. These records allow an agent to maintain continuity across multiple sessions and avoid revisiting decisions unnecessarily.

These categories are intended to illustrate different ways of providing context to an AI agent, rather than represent an exhaustive or formally established classification.

### Persistent instructions

Persistent instructions are commonly stored in Markdown files, identified by the .md extension. When working with an AI agent that reads and writes files in a directory, it is common to find an instruction file named AGENTS.md or CLAUDE.md, depending on the agent being used. These files provide instructions that the agent can apply consistently across multiple sessions. Over time, users can develop and refine these instructions based on their experience of working with agents.
Examples of extracts from my own CLAUDE.md files include:

    ```
    Assume I'm a generalist, not an expert. I tend to know a little about a lot of things. If I suggest a particular approach, don't just follow it — tell me how an expert in that field would tackle the same problem. Flag best practices, common pitfalls, and established patterns I might not be aware of. Help me learn as we go, don't just ship.
    ```
And:

    ```
    Before considering something done, check it on two dimensions:

    - Does it work? Does the system behave correctly and robustly?
    - Does it work for people? Consider the full range of users. Is it inclusive, accessible, and appropriate for its context? If the audience includes students, is it pedagogically sound and clear? If it's public-facing, is it welcoming and respectful of different backgrounds and abilities?
    ```

Persistent instructions can also include
* the objectives of a project,
* strategic design decisions, 
* conventions to be followed, 
* preferred software tools and technologies,
* the architecture of the intended output,
* methods for validating the work undertaken.

Persistent instruction files can be extensive and detailed, sometimes exceeding 1,000 lines of text. Of course, AI itself can be particularly useful in developing and refining these instructions, helping to establish clear conventions, identify gaps and improve their effectiveness over time. Care should be taken to avoid unnecessarily lengthy or conflicting instructions, which can increase token consumption and reduce the effectiveness of the agent. 

### Record keeping

Record keeping is particularly important when working with AI agents. During long-horizon tasks, an agent can generate more files and lines of code than a human could realistically be expected to read and fully understand. Maintaining comprehensive documentation manually can be time-consuming, whereas an AI agent can generate and update records as part of its normal workflow. However, care should be taken to ensure that these records remain accurate and consistent with the work undertaken. Including explicit requirements for maintaining and updating documentation in the agent's persistent instructions can help mitigate this risk.

### Example of automated record keeping

<div class="admonition example">
  <p class="admonition-title">Example</p>
  <p>Consider using an AI agent to create a series of engineering reports containing images and diagrams that could be reused across multiple documents. It may be beneficial to maintain a central index recording which images are used in each report, along with their captions and alternative text (alt-text). This would allow a user or an AI agent to quickly identify which images appear in which documents, without needing to examine each report individually. This index, along with other records, would need to be kept up to date, either periodically or as new content is created or existing content is modified.</p>
</div>

Records of previous work can provide valuable context for an AI agent, particularly when they are retrieved in a future session or by a different agent. This is discussed further in the next section.

### Model context and the context window

AI models are trained on large quantities of data, from which they learn patterns, relationships and information that enable them to perform a wide range of tasks. This provides a foundation of knowledge and capabilities that can be used without supplying additional information. For example, an AI model will typically be able to write JavaScript functions or explain the Navier–Stokes equations without needing to be provided with reference material.

However, when using an AI model for a specific task, additional information is often required. This might include company policies, technical specifications, project requirements or information about the intended users of a product. This information can be provided to the model as *context*.

An AI model has a finite **context window**, which determines how much information it can consider at any one time. This can be thought of as a form of working memory, containing the instructions, information, conversation history and results of previous actions that are available to the model as it undertakes a task. The context window is measured in tokens, and its size varies between models.

Unlike the knowledge acquired during training, information provided through the context window is not permanently learned by the model. During long-horizon tasks, the context window can gradually fill as the agent reads files, executes commands and receives new information. To allow the agent to continue working, some agentic tools use a process called **compaction**, in which information from the existing context is summarised or compressed to reduce the number of tokens required. Although this allows the task to continue, some details may be lost during the process.

Context may also be lost when an agent session ends or when work is transferred to another model, depending on the capabilities of the agentic tool. This is why persistent instructions, record keeping and well-structured documentation are particularly important. By storing important information outside the context window, an agent can retrieve it during a future session and continue working with an understanding of the project's objectives, previous decisions and progress. Maintaining concise, relevant records also helps to minimise the number of tokens required to restore this context.

## Model Context Protocol (MCP)

Model Context Protocol (MCP) is an open standard that allows AI agents to connect to external software, tools and data sources. This enables an agent to interact with specialist software without the user needing to understand how to operate it directly. For example, an agent could be tasked with designing a component in CAD software, exporting the model and preparing it for manufacture using a 3D printer, with minimal human intervention.

<div class="admonition example">
  <p class="admonition-title">Example</p>
  <p>Creating CAD models using AI
  
  An example of my own use of MCP involved connecting Autodesk Fusion 360 to the Claude desktop application. I produced a pencil sketch of an engineering component, including its dimensions, photographed the sketch and uploaded the image to Claude. I then instructed the agent to create a three-dimensional model of the component in Fusion 360. Once created, I was able to make further changes to the model through natural-language instructions in Claude, without needing to interact directly with the Fusion 360 interface.</p>
</div>

