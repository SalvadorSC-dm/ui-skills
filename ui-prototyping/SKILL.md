---
name: ui-prototyping
description: Rapidly prototype UI layouts and explore visual design options. Use when user asks to prototype, explore UI options, create design variants, or experiment with different visual approaches.
---

# UI Prototyping Skill

This skill enables rapid visual and layout exploration for the Leon App, focusing on generating design variants for comparison without production constraints.

## Critical: Branch Protection

**⚠️ NEVER work on the main branch!**

Before starting any prototyping work:

1. **Check the current branch** - If on `main` or `master`, you MUST stop
2. **Politely insist on creating a branch** - Explain that prototyping should never happen on main
3. **Suggest branch creation** - "I'd be happy to help with prototyping! However, we should work on a feature branch rather than main. Would you like me to help you create a branch, or would you prefer to create one yourself?"
4. **Do not proceed** until the user is on a non-main branch
5. **If user insists on main** - Continue politely explaining: "I understand, but prototyping work should be done on a feature branch to keep main stable. Could we create a branch like `prototype/[feature-name]`?"

**This is non-negotiable** - Prototyping is experimental and should never risk the main branch.

## When to Use

Activate this skill when:

- User asks to "prototype" or "explore" UI approaches
- User wants to "see different options" or "design variants"
- User mentions "no designs yet" or "not sure about layout"
- User wants to experiment with visual presentation
- User asks "what are some ways to display this?"
- Early design phase requiring visual exploration

## Scope & Philosophy

**Focus on:**

- ✅ Visual layout and hierarchy
- ✅ Component selection and combination
- ✅ Interaction patterns (click, hover, expand)
- ✅ Information density and organization
- ✅ Rapid iteration and comparison

**Don't worry about:**

- ❌ Accessibility (aria labels, keyboard nav)
- ❌ Production code quality
- ❌ i18n during prototyping
- ❌ Performance optimization
- ❌ Comprehensive error handling
- ❌ Test coverage

**Speed over perfection** - Build fast, show options, refine based on feedback.

## Prototyping Workflow

### 1. Understand the Context

Before generating variants:

- What needs to be displayed? (data, actions, relationships)
- What's the primary user goal?
- Any constraints? (data volume, screen size, existing patterns)
- What aspect needs exploration? (layout? interaction? visual style?)

**Ask clarifying questions if unclear.**

### 2. Propose Variant Strategy

Suggest how many variants to create:

- **2 variants** - Simple styling choices or tight constraints
- **3-4 variants** - Most UI exploration (default)
- **5+ variants** - Fundamental pattern exploration or user requests broad options

**Example:**

> "I'll create 3 variants exploring different information densities: compact table, card grid, and split-pane view. Sound good?"

**Wait for user confirmation before implementing.**

### 3. Generate Meaningful Variants

Create variants that differ in meaningful ways:

**Explore different dimensions:**

- Information density (compact vs spacious)
- Component choice (List vs Table vs Cards)
- Visual hierarchy (what's emphasized)
- Interaction pattern (inline vs modal vs expand)
- Layout strategy (grid vs list vs split-view)

**Label descriptively:**

- ✅ "Compact Table with Inline Actions"
- ✅ "Card Grid with Hover Preview"
- ✅ "Collapsible Sections by Category"
- ❌ "Option A", "Option B" (too generic)

### 4. Implement in Prototypes Folder

**File organization:**

```
src/
  app/
    dashboard/
      page.tsx
      prototypes/
        layout-variants.tsx        ← Create here
  components/
    UserList/
      UserList.tsx
      prototypes/
        list-display-options.tsx   ← Create here
```

**Variant switcher pattern:**

Always include a draggable variant picker in your prototypes. It floats over the UI so it doesn't affect the page layout.

```tsx
"use client";

import { useState } from "react";
import { DraggableVariantPicker } from "@/components/prototypes/draggable-variant-picker";

// Define your variant type, for example:
type VariantType = "compact" | "cards" | "split";

// Your prototype component
export function LayoutVariants() {
  const [variant, setVariant] = useState<VariantType>("compact");

  return (
    <>
      {/* Draggable variant picker - floats over UI, can be moved */}
      <DraggableVariantPicker
        value={variant}
        onChange={setVariant}
        options={[
          { label: "Compact Table", value: "compact" },
          { label: "Card Grid", value: "cards" },
          { label: "Split View", value: "split" },
        ]}
      />

      {/* Your prototype content */}
      <div className="p-6">
        {variant === "compact" && <CompactTableVariant data={mockData} />}
        {variant === "cards" && <CardGridVariant data={mockData} />}
        {variant === "split" && <SplitViewVariant data={mockData} />}
      </div>
    </>
  );
}
```

**Simple rules:**

- ✅ Import `DraggableVariantPicker` from `@/components/prototypes/draggable-variant-picker`
- ✅ Pass your variant options as props
- ✅ It floats over the UI and can be dragged around
- ✅ Keeps prototypes clean and non-intrusive

### 5. Provide Analysis

For each variant, include analysis (as comments or markdown):

```tsx
/**
 * COMPACT TABLE VARIANT
 *
 * Pros:
 * - High information density, many items visible
 * - Sortable columns for data exploration
 * - Familiar pattern for data-heavy interfaces
 *
 * Cons:
 * - Can feel cramped on smaller screens
 * - Less visual appeal, more utilitarian
 * - Harder to scan for specific items
 *
 * Best for:
 * - Power users needing to process lots of data
 * - Desktop-first workflows
 * - When sorting/filtering is primary interaction
 */
```

### 6. Suggest Improvements (Optional)

If you see opportunities beyond the request:

- **Describe in chat first**, don't implement yet
- Explain the potential benefit
- **Wait for user approval** before adding

**Example:**

> "I notice all variants could benefit from quick filters at the top. Would you like me to add that to the variants, or keep it simpler for now?"

### 7. Iterate & Refine

After user selects a variant:

- Refine based on feedback
- Polish the visual design
- Prepare for production handoff (add i18n, types, real API)

## Mock Data Strategy

**Use mock data liberally:**

```tsx
// Simple mock
const MOCK_USERS = [
  { id: 1, name: "Alice Chen", role: "Admin", status: "active" },
  { id: 2, name: "Bob Smith", role: "User", status: "inactive" },
];

// Large dataset simulation
const MOCK_LARGE = Array.from({ length: 100 }, (_, i) => ({
  id: i,
  name: `User ${i}`,
  createdAt: new Date(Date.now() - i * 86400000).toISOString(),
}));

// Different scenarios
const MOCK_EMPTY = [];
const MOCK_SINGLE = [{ id: 1, name: "Only User" }];
```

**When to use real data:**

- User specifically requests it
- Data structure significantly affects design
- Demonstrating actual API integration

## Common Prototyping Patterns

Quick reference for common UI patterns:

### Data Visualization

- **Master-Detail** - List + side panel for selected item
- **Card Grid** - Equal-sized cards in responsive grid
- **Expandable Rows** - Table with expandable detail rows
- **Tabbed Categories** - Tabs to switch between data types

### Interaction Patterns

- **Hover Preview** - Popover/Tooltip on hover
- **Click to Expand** - Accordion/Collapse for details
- **Inline Editing** - Edit directly in table/list
- **Modal Details** - Click to open full detail modal

### Filter/Search Patterns

- **Top Bar Filters** - Horizontal filter row above content
- **Sidebar Filters** - Vertical filter panel alongside content
- **Search + Tags** - Search bar with clickable filter tags
- **Quick Switch** - Segmented control for category switching

Use these as starting points, not prescriptions.

## Anti-Patterns

Avoid wasting time on:

❌ **Over-engineering** - Don't build complex state management for prototypes
❌ **Premature optimization** - Skip memoization, virtualization, lazy loading
❌ **Perfect types** - `any` is fine for rapid iteration
❌ **Edge cases** - Focus on happy path first
❌ **Pixel perfection** - Close enough is good enough
❌ **Feature creep** - Stick to the exploration goal
❌ **Production concerns** - Don't worry about accessibility, i18n, tests yet

✅ **Instead:** Build fast → Show options → Get feedback → Iterate

## Ant Design Component Toolkit

You have the full Ant Design 6 library:

**Commonly useful:**

- `Table`, `List` - Data display
- `Card`, `Descriptions` - Content containers
- `Tag`, `Badge` - Labels and counts
- `Collapse`, `Tabs`, `Segmented` - Organization
- `Divider`, `Space` - Layout
- `Empty` - Empty states
- `Popover`, `Tooltip` - Contextual info

**Tips:**

- Combine components creatively (Card + Collapse, List + Descriptions)
- Use Tailwind for layout (`grid`, `flex`, `space-y-4`)
- Check [Ant Design docs](https://ant.design/components) for inspiration
- Customize with `className` for unique looks

## Prototyping Shortcuts

**These are OK in prototypes** (fix before production):

✅ Hardcoded strings (no i18n)
✅ `any` types where typing is complex
✅ Inline styles for quick adjustments
✅ Mock data instead of API
✅ Skip loading/error states
✅ Console logs for debugging
✅ No accessibility attributes

**Still avoid:**
❌ Breaking existing features
❌ Modifying production files directly
❌ Committing broken code

## Tech Stack Quick Reference

**State:**

```tsx
const [variant, setVariant] = useState<"a" | "b">("a");
```

**Styling:**

```tsx
className="p-4 space-y-4 grid grid-cols-2 gap-4"
<Card className="shadow-sm border-0" />
```

**Icons:**

```tsx
import { User, Filter } from "lucide-react";
<User size={16} />;
```

## Transition to Production

When user is ready to move forward:

### Refine Chosen Variant

- Add i18n: Use `useTranslations` from `next-intl`
- Add types: Remove `any`, add proper interfaces
- Real data: Replace mock with TanStack Query
- Add states: Loading, error, empty states
- Add accessibility: ARIA labels, keyboard nav
- Clean code: Remove debug logs, unused code

### Move to Final Location

- Copy from `/prototypes` to production location
- Update imports and file references
- Integrate with existing codebase

### Hand Off

- Mention it's from a prototype
- Highlight remaining production work
- Note any edge cases to handle
- Keep prototype file as reference (delete later)

## Examples

### Example 1: Layout Exploration

**User:** "Show conditional dimension usage - no designs yet"

**Response:**

1. Understand: Need to display `{ bidder: [], publisher: [], csts: [], creatives: [] }`
2. Propose: "I'll create 3 variants: compact tags, expandable sections, and tabbed view. Good?"
3. Implement in `prototypes/dimension-usage-variants.tsx`
4. Provide pros/cons for each
5. User selects expandable sections
6. Refine with real data and i18n

### Example 2: List Display

**User:** "Prototype different ways to show user list"

**Response:**

1. Understand: Display users with actions
2. Propose: "4 variants exploring density: data table, card grid, compact list, split view?"
3. Implement with mock users
4. Show comparison
5. Suggest: "Add search bar to all variants?"
6. Refine chosen approach

## Communication Style

- **Show, don't tell** - Build so users can see/interact
- **Explain trade-offs** - Why each has pros/cons
- **Iterate quickly** - Fast builds, quick feedback cycles
- **Suggest proactively** - But always ask before implementing
- **Check branch first** - Never work on main, insist on feature branch

## Critical Reminders

Before starting any prototyping work:

1. ⚠️ **Check branch** - If on `main` or `master`, stop and insist on creating a feature branch
2. ✅ **Always include DraggableVariantPicker** - Import from `@/components/prototypes/draggable-variant-picker`
3. ✅ **Pass options as props** - Makes it reusable and generic
4. ✅ **Floats over UI** - Non-intrusive, can be dragged around

---

**Remember:** Your goal is rapid visual exploration, not production code. Build fast, show options, enable informed decisions. But always protect the main branch and make prototypes work with the draggable variant picker.
