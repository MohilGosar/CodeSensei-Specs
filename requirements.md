# Requirements Document: CodeSensei

## Introduction

CodeSensei is an AI-driven refactoring coach VS Code extension that provides real-time code analysis and personalized learning experiences. The system monitors student code, detects learning opportunities, and delivers interactive micro-lessons and refactoring guidance directly within the IDE. Unlike generic autocomplete tools, CodeSensei acts as a virtual sensei, transforming code quality issues into educational moments.

## Glossary

- **CodeSensei_Extension**: The VS Code extension component that provides the user interface and IDE integration
- **Analysis_Service**: The Python-based backend service that performs code analysis and pattern detection
- **AST_Parser**: The Abstract Syntax Tree parser that analyzes code structure
- **Learning_Moment**: A detected code pattern or issue that presents an educational opportunity
- **Micro_Lesson**: An interactive educational module triggered by a learning moment
- **Refactoring_Sandbox**: An interactive environment where users can explore refactoring options
- **Learning_Analytics_Dashboard**: A visual interface displaying user progress and metrics
- **Issue_Classifier**: The component that categorizes detected code issues
- **LLM_Service**: The Large Language Model integration for generating lessons and explanations
- **Decorator_API**: VS Code API for highlighting code in the editor
- **Local_Cache**: Storage mechanism for preventing repetitive tips and improving performance
- **Skill_Tag**: A categorization label for tracking specific programming competencies

## Requirements

### Requirement 1: Real-Time Code Analysis

**User Story:** As a student developer, I want my code to be analyzed in real-time, so that I can receive immediate feedback on potential improvements.

#### Acceptance Criteria

1. WHEN a user edits code in the VS Code editor, THE AST_Parser SHALL parse the code within 200ms of the last keystroke
2. WHEN the AST_Parser detects a code pattern, THE Analysis_Service SHALL classify the pattern within 100ms
3. THE AST_Parser SHALL detect long functions exceeding 50 lines of code
4. THE AST_Parser SHALL detect magic numbers that are not defined as named constants
5. THE AST_Parser SHALL detect inefficient loop patterns including nested loops with O(n²) or higher complexity
6. THE AST_Parser SHALL detect duplicated code blocks with 5 or more identical consecutive lines
7. WHEN parsing fails due to syntax errors, THE AST_Parser SHALL handle the error gracefully and continue monitoring
8. THE Analysis_Service SHALL process code analysis without blocking the VS Code editor UI thread

### Requirement 2: Issue Classification System

**User Story:** As a student developer, I want detected issues to be categorized by type, so that I can understand what aspect of coding I need to improve.

#### Acceptance Criteria

1. WHEN a code pattern is detected, THE Issue_Classifier SHALL assign it to exactly one category
2. THE Issue_Classifier SHALL support the category "Syntax Basics" for fundamental language syntax issues
3. THE Issue_Classifier SHALL support the category "Logic Clarity" for code readability and maintainability issues
4. THE Issue_Classifier SHALL support the category "Performance" for efficiency and optimization opportunities
5. THE Issue_Classifier SHALL support the category "Readability" for code style and documentation issues
6. THE Issue_Classifier SHALL support the category "Security" for potential security vulnerabilities
7. WHEN classification confidence is below 70%, THE Issue_Classifier SHALL assign the issue to the most likely category and log the uncertainty

### Requirement 3: Micro-Lesson Delivery

**User Story:** As a student developer, I want to receive interactive lessons when issues are detected, so that I can learn why the issue matters and how to fix it.

#### Acceptance Criteria

1. WHEN a Learning_Moment is detected, THE CodeSensei_Extension SHALL display a micro-lesson in a side panel within 500ms
2. THE Micro_Lesson SHALL display a before snippet showing the user's actual problematic code
3. THE Micro_Lesson SHALL display an after snippet showing the improved version of the code
4. THE Micro_Lesson SHALL include 2 to 3 bullet points explaining the improvement
5. THE Micro_Lesson SHALL include a 30-second multiple-choice quiz with 3 to 4 answer options
6. WHEN a user completes a quiz, THE CodeSensei_Extension SHALL provide immediate feedback indicating correct or incorrect answers
7. WHEN a user answers correctly, THE Learning_Analytics_Dashboard SHALL record the successful completion
8. THE LLM_Service SHALL generate lesson content that is contextually relevant to the detected code pattern

### Requirement 4: Visual Code Highlighting

**User Story:** As a student developer, I want learning moments to be visually highlighted in my code, so that I can easily identify where improvements can be made.

#### Acceptance Criteria

1. WHEN a Learning_Moment is detected, THE CodeSensei_Extension SHALL use the Decorator_API to highlight the relevant code
2. THE CodeSensei_Extension SHALL display gutter icons for detected learning moments
3. THE CodeSensei_Extension SHALL display inline decorations for detected learning moments
4. WHEN a user hovers over a highlighted code section, THE CodeSensei_Extension SHALL display a tooltip with a brief description
5. THE CodeSensei_Extension SHALL use distinct colors for different issue categories
6. WHEN a user clicks on a gutter icon, THE CodeSensei_Extension SHALL open the corresponding micro-lesson in the side panel

### Requirement 5: Refactoring Sandbox

**User Story:** As a student developer, I want to explore different refactoring options for my code, so that I can understand trade-offs and choose the best approach.

#### Acceptance Criteria

1. WHEN a user selects a code block and invokes the refactoring command, THE Refactoring_Sandbox SHALL display within 1 second
2. THE Refactoring_Sandbox SHALL present 1 to 3 refactoring variants for the selected code
3. WHEN displaying refactoring variants, THE Refactoring_Sandbox SHALL include trade-off explanations for each variant
4. THE Refactoring_Sandbox SHALL label trade-offs with dimensions including "Readability," "Performance," "Maintainability," and "Simplicity"
5. WHEN a user selects a refactoring variant, THE CodeSensei_Extension SHALL provide a one-click apply button
6. WHEN a user clicks the apply button, THE CodeSensei_Extension SHALL replace the selected code with the chosen variant
7. WHEN a refactoring is applied, THE CodeSensei_Extension SHALL create an undo point in the editor history
8. THE LLM_Service SHALL generate refactoring variants that are syntactically correct and functionally equivalent to the original code

### Requirement 6: Local Caching System

**User Story:** As a student developer, I want the extension to remember which tips I've already seen, so that I don't receive repetitive feedback on the same issues.

#### Acceptance Criteria

1. WHEN a Learning_Moment is displayed to a user, THE Local_Cache SHALL record the code pattern and file location
2. WHEN a previously cached Learning_Moment is detected again in the same location, THE CodeSensei_Extension SHALL suppress the notification
3. THE Local_Cache SHALL expire cached entries after 7 days
4. WHEN a user explicitly dismisses a Learning_Moment, THE Local_Cache SHALL record the dismissal permanently for that location
5. THE Local_Cache SHALL store data in the VS Code workspace storage
6. WHEN the cache size exceeds 10MB, THE Local_Cache SHALL remove the oldest entries first

### Requirement 7: Learning Analytics Dashboard

**User Story:** As a student developer, I want to track my progress and improvements over time, so that I can see how my coding skills are developing.

#### Acceptance Criteria

1. THE Learning_Analytics_Dashboard SHALL display skill tags including "OOP," "Error Handling," "Performance Optimization," "Code Readability," and "Security Practices"
2. WHEN a user completes a micro-lesson quiz, THE Learning_Analytics_Dashboard SHALL update the corresponding skill tag progress
3. THE Learning_Analytics_Dashboard SHALL display a "Lines Saved" metric showing cumulative lines removed through refactoring
4. THE Learning_Analytics_Dashboard SHALL display a "Cyclomatic Complexity Improved" metric showing complexity reduction
5. THE Learning_Analytics_Dashboard SHALL display a timeline chart showing progress over the last 30 days
6. WHEN a user applies a refactoring, THE Learning_Analytics_Dashboard SHALL calculate and record the metric improvements
7. THE Learning_Analytics_Dashboard SHALL persist data across VS Code sessions
8. WHEN a user opens the dashboard, THE CodeSensei_Extension SHALL load and display the data within 500ms

### Requirement 8: Performance Optimization

**User Story:** As a student developer, I want the extension to run smoothly without slowing down my IDE, so that I can maintain my coding flow.

#### Acceptance Criteria

1. THE AST_Parser SHALL process files incrementally, analyzing only changed code sections
2. WHEN a file exceeds 1000 lines, THE AST_Parser SHALL use a debounce delay of 500ms before analyzing
3. WHEN a file is under 1000 lines, THE AST_Parser SHALL use a debounce delay of 200ms before analyzing
4. THE Analysis_Service SHALL limit concurrent analysis requests to 3 per workspace
5. THE CodeSensei_Extension SHALL consume less than 100MB of memory during normal operation
6. THE CodeSensei_Extension SHALL not increase VS Code startup time by more than 200ms
7. WHEN the system detects performance degradation, THE CodeSensei_Extension SHALL automatically reduce analysis frequency

### Requirement 9: Extension Configuration

**User Story:** As a student developer, I want to customize the extension's behavior, so that it fits my learning style and preferences.

#### Acceptance Criteria

1. THE CodeSensei_Extension SHALL provide a settings panel accessible from VS Code preferences
2. WHERE the user enables "Aggressive Mode," THE CodeSensei_Extension SHALL show all detected learning moments immediately
3. WHERE the user enables "Gentle Mode," THE CodeSensei_Extension SHALL show only high-priority learning moments
4. THE CodeSensei_Extension SHALL allow users to disable specific issue categories
5. THE CodeSensei_Extension SHALL allow users to adjust the minimum function length threshold for detection
6. THE CodeSensei_Extension SHALL allow users to enable or disable quiz generation
7. WHEN a user changes settings, THE CodeSensei_Extension SHALL apply the changes immediately without requiring a restart

### Requirement 10: Backend API Integration

**User Story:** As a system architect, I want a well-defined API contract between the extension and backend, so that components can be developed and tested independently.

#### Acceptance Criteria

1. THE CodeSensei_Extension SHALL communicate with the Analysis_Service via HTTP REST API
2. WHEN sending code for analysis, THE CodeSensei_Extension SHALL include the code content, file path, and language identifier
3. THE Analysis_Service SHALL respond to analysis requests with detected patterns, classifications, and confidence scores
4. WHEN requesting lesson generation, THE CodeSensei_Extension SHALL send the code pattern and issue category to the LLM_Service
5. THE LLM_Service SHALL respond with lesson content including before/after snippets, explanations, and quiz questions
6. WHEN the Analysis_Service is unavailable, THE CodeSensei_Extension SHALL display a user-friendly error message and continue operating in degraded mode
7. THE API SHALL use JSON for all request and response payloads
8. THE API SHALL include version headers to support backward compatibility

### Requirement 11: User Progress Persistence

**User Story:** As a student developer, I want my learning progress to be saved, so that I can continue my learning journey across sessions and devices.

#### Acceptance Criteria

1. WHEN a user completes a quiz or applies a refactoring, THE CodeSensei_Extension SHALL persist the event to local storage
2. THE CodeSensei_Extension SHALL store user progress data in JSON format
3. WHEN VS Code starts, THE CodeSensei_Extension SHALL load user progress data within 100ms
4. THE CodeSensei_Extension SHALL support exporting user progress data to a file
5. THE CodeSensei_Extension SHALL support importing user progress data from a file
6. WHEN importing progress data, THE CodeSensei_Extension SHALL merge it with existing data without overwriting newer entries

### Requirement 12: Multi-Language Support

**User Story:** As a student developer, I want the extension to support multiple programming languages, so that I can learn across different technology stacks.

#### Acceptance Criteria

1. THE AST_Parser SHALL support parsing TypeScript code
2. THE AST_Parser SHALL support parsing JavaScript code
3. THE AST_Parser SHALL support parsing Python code
4. WHEN a file with an unsupported language is opened, THE CodeSensei_Extension SHALL display a notification indicating limited support
5. THE Issue_Classifier SHALL apply language-specific rules when categorizing issues
6. THE LLM_Service SHALL generate lessons appropriate for the detected programming language
