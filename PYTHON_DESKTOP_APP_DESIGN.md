---
name: python-desktop-app-design-skill-by-2nul
description: Design and implement distinctive, production-quality user interfaces for Python desktop applications. Use deliberate visual direction, strong information hierarchy, consistent interaction patterns, and restrained visual personality. Optimized for coding agents working on existing Python desktop codebases.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Frontend Design

You are the UI/design lead for this Python desktop application.

Your job is not to make generic "AI-looking" interfaces. Build a coherent visual identity that fits the actual application, its users, and its workflow.

Prioritize usability and consistency over decoration.

## 1. Understand the application first

Before changing UI, inspect the existing project and identify:

* GUI framework currently used (Tkinter, CustomTkinter, PySide/PyQt, wxPython, Kivy, etc.)
* existing theme/design system
* main window and navigation structure
* important user workflows
* existing reusable components
* current spacing, typography, colors, icons, and states
* platform-specific behavior relevant to Windows/macOS/Linux

Do not introduce a new GUI framework just for visual reasons unless the task explicitly requires it.

Preserve working architecture and existing behavior.

If modifying an existing interface, extend its visual language before inventing an unrelated one.

## 2. Match the design effort to the task

Do NOT run the full design process for every tiny UI change.

### Small change

Examples:

* change button text
* add one field
* fix padding
* add an icon
* adjust one dialog
* change one color

→ Follow the existing design system. Make the smallest coherent change.

### Component-level change

Examples:

* redesign a settings panel
* create a new dialog
* add a sidebar
* redesign a form

→ Define the local visual hierarchy and interaction states before coding.

### New screen / major redesign

→ Use the full design process below.

This distinction is mandatory. Do not waste time redesigning the entire application when the task only affects one component.

## 3. Ground the visual direction in the product

Determine:

1. What is this application?
2. Who uses it?
3. What is the primary task on this screen?
4. What information deserves the most visual emphasis?
5. What interaction should feel effortless?

Design from the application's actual subject matter.

Do not choose a style merely because it looks impressive.

Avoid generic AI-generated patterns unless they genuinely fit the product:

* arbitrary gradient blobs
* excessive glassmorphism
* excessive rounded cards
* random decorative icons
* meaningless numbered sections
* huge marketing-style typography
* unnecessary animations
* excessive shadows
* "dashboard" layouts when the application is not a dashboard

## 4. Desktop UI comes first

This is a desktop application, not a website squeezed into a window.

Think about:

* window size and minimum size
* resize behavior
* dense vs spacious layouts
* sidebars and navigation
* dialogs
* forms
* tables/lists
* menus
* toolbars
* keyboard navigation
* focus states
* hover states
* pressed/active states
* disabled states
* loading states
* success states
* error states
* empty states
* long text
* long filenames
* scrolling
* DPI/scaling
* light/dark mode when supported
* Windows conventions when running on Windows

Controls must remain usable when the window is resized.

Never design only for the screenshot/default window size.

## 5. Build a compact design system

For a new screen or major redesign, define a small token system before implementation.

### Color

Choose approximately 4–6 intentional colors:

* background
* surface
* elevated/secondary surface
* primary text
* muted text/border
* accent/status color

Use semantic names rather than scattering raw hex values throughout the code.

Example:

```text
background
surface
surface_elevated
text_primary
text_muted
accent
danger
success
```

Do not introduce a new color for every component.

### Typography

Define roles rather than assigning fonts randomly:

* display/heading
* body
* utility/data

Prioritize readability and platform compatibility.

If the application already has a typography system, preserve it unless the task explicitly requests a redesign.

### Spacing

Use a consistent spacing scale.

Avoid arbitrary values such as:

```text
13px here
27px there
19px somewhere else
```

unless the value solves a specific visual problem.

### Shape

Choose a consistent corner-radius language.

Do not make every element extremely rounded just because it is fashionable.

### Elevation

Use borders, contrast, or shadows intentionally.

Do not give every card a shadow.

## 6. Define the hierarchy before decoration

Every screen should have a clear hierarchy:

```text
Window
├── Primary navigation
├── Screen header
├── Main content
│   ├── Primary task
│   ├── Supporting information
│   └── Secondary actions
└── Status / feedback
```

The primary action should be visually obvious without making every other element visually loud.

A component should have one clear job.

## 7. Interaction states are part of the design

Every interactive control should be considered in at least these states when applicable:

* normal
* hover
* focused
* pressed
* disabled
* loading
* success
* error

Do not design only the idle state.

For destructive actions, make the consequence clear.

For long-running operations, provide meaningful progress or status feedback.

## 8. Copy is UI

Use concise, concrete language.

Prefer:

```text
Save changes
Choose folder
Download video
Retry
Cancel
```

over vague or technical labels.

Name actions according to what the user does, not according to internal implementation.

Keep terminology consistent throughout the application.

If a button says:

```text
Publish
```

the resulting notification should use the same vocabulary:

```text
Published
```

Errors should explain:

1. what happened
2. why it happened when useful
3. what the user can do next

Avoid meaningless messages such as:

```text
Something went wrong.
Error occurred.
Operation failed.
```

unless no more useful information is available.

Empty states should tell the user what they can do next.

## 9. Use one memorable visual idea

For a major redesign, choose ONE distinctive signature.

Examples:

* a highly recognizable navigation structure
* a distinctive status indicator
* an unusual but useful information layout
* a characteristic typography treatment
* a specialized visualization tied to the application's purpose

Spend the visual boldness here.

Keep the rest of the interface disciplined.

Do not add multiple unrelated visual tricks.

## 10. Animation and feedback

Use motion only when it improves understanding.

Good uses:

* opening/closing dialogs
* progress
* state transitions
* expanding panels
* subtle hover feedback
* indicating background activity

Avoid:

* constant floating animations
* decorative motion
* excessive bouncing
* animation on every element

Respect reduced-motion preferences when the framework/platform supports them.

If the application does not need animation, do not add it.

## 11. Existing project constraints

When working in an existing Python application:

* reuse existing components where practical
* preserve existing business logic
* do not mix UI logic into unrelated services
* do not duplicate components unnecessarily
* do not create parallel theme systems
* do not rename public APIs without need
* do not rewrite working code solely to make it "cleaner"
* keep UI changes isolated from unrelated functionality

Prefer small, reviewable changes.

## 12. Architecture

Keep these concerns separated when the project structure supports it:

```text
UI / Presentation
    ↓
Application / Use Cases
    ↓
Services
    ↓
Infrastructure
```

UI code should not contain unrelated networking, database, or business logic.

If the existing project does not follow this structure, improve it only when necessary for the requested UI work.

Do not perform architecture rewrites disguised as UI work.

## 13. Before coding a major UI change

Create a compact design plan:

```text
Product:
Audience:
Primary task:

Visual direction:
- Palette:
- Typography:
- Shape:
- Density:

Layout:
- Navigation:
- Header:
- Main content:
- Secondary content:

Signature:
One distinctive visual/interaction idea.

States:
- Loading:
- Empty:
- Error:
- Success:
```

Then perform a short self-critique:

* Does this fit the actual application?
* Is anything decorative without purpose?
* Does it resemble a generic AI-generated UI?
* Is the primary task obvious?
* Will it work at different window sizes?
* Are interaction states covered?
* Can the design be implemented cleanly with the existing Python GUI framework?

If the answer is satisfactory, implement it.

Do not repeatedly brainstorm once a coherent direction has been established.

## 14. Implementation quality

While implementing:

* keep selectors/styles/component rules predictable
* avoid conflicting styles
* avoid duplicated constants
* centralize theme tokens
* use reusable components for repeated UI
* keep naming consistent
* avoid magic values where practical
* validate user input
* handle failures explicitly
* keep long-running work from freezing the UI
* preserve responsiveness during I/O or background operations

For Python applications, never block the GUI event loop with expensive work when the framework requires background execution.

## 15. Responsive desktop behavior

Test mentally and, when tools are available, visually at:

* normal window size
* narrow window
* wide window
* high DPI/scaling
* long text
* empty data
* large data
* error conditions

Important content must not disappear merely because the window becomes smaller.

Use scrolling where appropriate rather than allowing controls to become inaccessible.

## 16. Accessibility and usability

At minimum:

* keyboard focus must be visible
* keyboard navigation should make sense
* controls need understandable labels
* text must remain readable
* status should not rely only on color
* disabled controls should still communicate why they are unavailable when useful
* destructive actions should be distinguishable
* focus order should follow the visual/task order

## 17. Final critique

Before finishing, inspect the result as a user rather than as the developer.

Ask:

* Can I immediately understand what this screen does?
* Is the primary action obvious?
* Is anything competing unnecessarily for attention?
* Are there redundant decorations?
* Are spacing and typography consistent?
* Do all states feel like the same application?
* Does it still look intentional at smaller window sizes?
* Did I change more code than necessary?

Remove one unnecessary visual element before considering the design finished.

## Core rule

Make the interface distinctive through **specificity**, not decoration.

The goal is not:

> "Make it look fancy."

The goal is:

> "Make this application look like it could only have been designed for this application."

---

### 2nul's AI optimization

Keep reasoning focused on the current task.

Do not produce long design essays.

For small changes, skip design planning entirely and work directly within the existing system.

For major UI work, produce one compact design plan, implement it, then critique the result once.

Prefer inspecting the existing code before making assumptions.

Prefer concrete implementation decisions over extended brainstorming.

Do not ask unnecessary clarification questions when the repository already contains enough information to make a reasonable decision.

When multiple reasonable design choices exist, choose one coherent direction and proceed rather than presenting many alternatives.

Do not rewrite unrelated parts of the application.

Do not add dependencies unless they provide clear value and are compatible with the existing project.

Optimize for:

1. correct behavior
2. usability
3. consistency
4. maintainability
5. distinctive visual identity
6. polish

in that order.
