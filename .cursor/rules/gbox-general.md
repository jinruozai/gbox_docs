# Gbox Game Engine General Rules

## Description
When I'm working with files related to the Gbox game engine, use this knowledge to provide better code assistance.

## Files
*.gb, *.gbz

## Rules

### Gbox Engine General Concepts
- Gbox is a lightweight 2D game engine with its own scripting language
- The file extensions for Gbox scripts are `.gb` and `.gbz`
- The scripting language has a C-like syntax but with specific game-oriented features
- Consider Gbox scripts as a domain-specific language designed for 2D game development
- Gbox scripts are used to define game objects, behaviors, UI elements, and game logic

### Code Generation Guidelines
- When generating or editing Gbox code, strictly follow the syntax documented in @doc/gbox_syntax.md
- Reference the API documentation in @doc/gbox_api.md for available classes, methods, and properties
- Always use proper variable naming conventions as specified in the syntax guide
- Prioritize using engine-provided classes and functions over reinventing functionality

### Code Analysis
- When analyzing Gbox code, pay attention to the inheritance hierarchy of classes
- Recognize standard Gbox patterns for game object creation and management
- Be aware of memory management considerations specific to Gbox
- Consider performance implications of different approaches in the context of 2D game development

### Additional Considerations
- Suggest optimizations specific to 2D game development when appropriate
- Recommend best practices for structuring Gbox game projects
- Help with debugging common issues in Gbox scripts 