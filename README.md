## CSS-Basics-Selectors
Assignment: CSS Basics and Selectors

# Question to GPT:

Please explain:

Why were some CSS selectors applying as expected, and what was the minimal fix?

# Answer provided:

Great question! This is about CSS specificity and inheritance.
Why Some Selectors Worked and Others Didn't
Worked fine:

section h2 - Already had explicit color: var(--primary-color);
section h4 - Already had explicit color: var(--secondary-color);
nav a - Already had explicit color: var(--text-dark);

Broke:

header h1, header p - Were relying on inheritance from header { color: white; }
They didn't have explicit color declarations of their own

The Problem: Inheritance vs. Direct Styles
When you added base styles like:
cssh1 { color: var(--text-dark); }
p { color: var(--text-light); }
These direct element styles override inherited colors because:

Inheritance has the lowest priority in CSS
Any direct style on an element beats inherited styles
So h1 { color: var(--text-dark); } beat the inherited color: white from the parent header

The Minimal Fix
Add explicit color declarations to the specific selectors:
css/* Before (broken) */
header h1 {
    font-size: 2.5rem;
    /* No color - was inheriting white from header */
}

/* After (fixed) */
header h1 {
    font-size: 2.5rem;
    color: white; /* Explicit declaration */
}
This works because of specificity:

header h1 (specificity: 0,0,2) beats h1 (specificity: 0,0,1)
More specific selectors always win

Key Takeaway: When adding base styles, always check if any elements rely on inheritance rather than explicit declarations, and add those explicit declarations to the more specific selectors.
