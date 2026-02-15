CodeSensei: An AI Refactoring Mentor

CodeSensei is a VS Code extension built to bridge the gap between writing code that simply works and writing code that is truly professional. It is designed for students and developers who are tired of blindly following AI suggestions and want to actually understand the "why" behind clean code.

The Philosophy:

Most AI tools today are built to replace the developer's thought process by providing instant answers. While that helps with speed, it often stalls growth. CodeSensei takes a different approach by acting as a quiet observer in your editor. It looks for moments where your code could be more efficient or readable and turns those moments into a conversation. Instead of just fixing the problem for you, it helps you learn how to fix it yourself.

The Experience:

The extension stays out of your way until it detects a specific pattern worth discussing—what we call a "Learning Moment." This could be a function that has grown too complex, a piece of logic that repeats itself, or a variable name that doesn't quite describe its purpose.
When you engage with a highlight, CodeSensei provides a focused explanation based on your actual code, not a generic example. To make sure the concept sticks, it generates a quick quiz using your own variable names. Once you've grasped the concept, you can explore different ways to refactor that block—comparing one version for speed and another for readability—before choosing the one you want to apply.

The Technical Foundation:

The system is built on a split architecture to keep the editor fast. The interface is a TypeScript-based VS Code extension that uses React to handle the lesson panels. Behind the scenes, a Python-based analysis engine uses Abstract Syntax Tree (AST) parsing to understand the structure of your work. We use Large Language Models to personalize the lessons, ensuring every quiz and explanation feels relevant to the specific project you are working on.
This entire project was mapped out using Spec-Driven Development in the Kiro IDE. By defining our requirements and design documents before writing a single line of feature code, we ensured that CodeSensei’s educational logic is consistent and reliable.

Project Structure:

You can find the core architectural documents for this project in the following files:
1. requirements.md: This document outlines the specific features and user stories we committed to building.
2. design.md: This covers the technical blueprint, including data schemas and the communication between the extension and the analysis engine.
