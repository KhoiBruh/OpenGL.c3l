# OpenGL.c3l

Ergonomic C3 bindings for OpenGL.

## Differences from raw bindings

This package modifies the raw generated bindings to remove friction from daily use in C3:

1. **Built-in Validation**: You do not need to check function pointers for `null` before calling them. `opengl::init(load)` validates that all core functions for the loaded version exist. If initialization succeeds, core function calls are safe.
2. **Typed Bitfields**: Constants like `GL_COLOR_BUFFER_BIT` are typed as `GLbitfield` instead of `GLenum`. You no longer need explicit casts like `(GLbitfield)GL_COLOR_BUFFER_BIT` when passing masks.
3. **Typed Booleans**: `GL_TRUE` and `GL_FALSE` are typed as `GLboolean`, avoiding implicit cast errors when interacting with boolean OpenGL parameters.

## Usage

```c3
import opengl;
import opengl::gl;

// Initialize once during startup using your platform's loader (e.g., SDL, GLFW)
if (catch err = opengl::init((GLLoadFn) &glfw::getProcAddress())) {
    // Handles missing context or missing core function pointers
    return err;
}

// Use safely without null checks or redundant type casts
gl::clearColor(0.08, 0.09, 0.1, 1.0);
gl::clear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

gl::bindBuffer(GL_ARRAY_BUFFER, vbo);
gl::vertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, null);
gl::enableVertexAttribArray(0);
```
