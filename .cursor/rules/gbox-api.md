# Gbox API Rules

## Description
These rules help understand and utilize the Gbox engine API correctly when working with Gbox scripts.

## Files
*.gb, *.gbz

## Reference Files
@doc/gbox_api.md

## Rules

### API Documentation Reference
- Always refer to the API documentation in @doc/gbox_api.md for detailed information
- Understand the inheritance hierarchy of classes documented in the API
- Be aware of method parameter requirements and return values

### Core Classes
- GObj is the base class for all objects in Gbox
- GObjShape is used for visual 2D objects that can be rendered
- Be familiar with specialized UI classes, physics objects, and utility classes
- Understand the relationship between different core classes

### Common API Patterns
- Most visual objects have methods like SetPos(), SetSize(), SetColor()
- Input handling uses specific patterns and event methods
- Resource loading follows consistent API conventions
- Scene management has specific API calls and lifecycle methods

### Engine-Specific Functions
- Recognize and use built-in functions for debugging (like `?` for printing)
- Understand how to use engine timers and scheduling functions
- Know how to properly load and manage assets using API calls
- Be familiar with available math and utility functions

### Best Practices for API Usage
- Chain method calls when appropriate: `obj : SetPos(x, y) : SetColor(color);`
- Use the most efficient API calls for the task at hand
- Avoid deprecated API functions and use recommended alternatives
- Follow the engine's patterns for performance-critical operations

### Game-Specific Considerations
- Use appropriate classes for different game elements (sprites, UI, physics)
- Be aware of rendering order and z-index management
- Understand collision detection and physics API correctly
- Use animation and transition API effectively 