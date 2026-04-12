# Claude Code Workflow: The Boris Cherny Method

**A structured, iterative system for mastering Claude Code beyond simple prompting.**

---

## Overview

This is a professional-grade workflow for using Claude Code effectively. Rather than jumping into coding, you adopt a disciplined system of planning, documentation, verification, and skill-building that scales across projects.

The key principle: **Your process matters more than your prompts as models improve.**

---

## 1. The Planning Phase (0:23 - 2:40)

Never jump straight into coding. Use **Plan Mode** (Shift + Tab twice) to force the AI to outline its logic first.

### Why This Matters
- Avoids the "quick-fix" trap where AI solves the wrong problem
- Prevents breaking existing code with shortsighted solutions
- Ensures alignment between your intent and AI's understanding

### Key Prompt for Planning
```
Interview me about this. What is the core problem this solves? 
Who is this for? What does success look like? 
And what should this NOT do? 
Summarize it back to me before you write any code.
```

### What to Look For
- Does the AI's plan align with your intended outcome?
- Is the plan too aggressive or does it skip critical logic?
- **If misaligned**: Redirect before execution begins—it's far cheaper to adjust a plan than to refactor code

### Best Practice
- Treat the planning phase as a separate, mandatory step
- Don't let urgency push you into skipping it
- Use this time to catch scope creep and edge cases

---

## 2. Managing `claude.md` (2:40 - 5:20)

Your `claude.md` file acts as your project's **operating system**. It contains all the context, constraints, and conventions Claude needs to know.

### The Biggest Mistake
Over-engineering it. Keep it short and focused.

### The Strategy
- If the model starts ignoring instructions or gets confused, **delete the file and start fresh**
- Too many rules = confusion and ignored instructions
- Better to have 5 clear, essential rules than 20 contradictory ones

### Proactive Maintenance Prompt
```
Update my `claude.md` to remove anything that is:
- No longer needed
- Contradictory
- Duplicate information
- Unnecessary bloat impacting effectiveness
```

### What Should Be in claude.md
- Project purpose and scope
- Key architectural decisions
- File structure and naming conventions
- Critical constraints (performance, security, compatibility)
- Code style guidelines
- Debugging/testing approach
- What the AI should NOT do

### What Should NOT Be in claude.md
- Micro-optimization tips
- Pedantic style rules (let the code speak)
- Redundant explanations of obvious concepts
- One-off workarounds (put these in comments, not the system file)

---

## 3. Verification Loops (5:20 - 6:53)

AI thrives when it can see the results of its actions. Verification closes the feedback loop.

### What to Provide
- Browser access (for web apps)
- Log files and error outputs
- Test results and coverage reports
- Real-time feedback on behavior

### Key Verification Prompt
```
Please go back and verify all of your work so far. 
Make sure you use best practices, were efficient, and didn't introduce any issues.
```

### Types of Verification
1. **Functional**: Does it work as intended?
2. **Performance**: Is it efficient (speed, memory, network)?
3. **Quality**: Are best practices applied (error handling, logging, tests)?
4. **Integration**: Does it break existing code or dependencies?

### How to Set Up Verification
- Automated test runs (unit tests, integration tests)
- Browser screenshots/recordings for UI work
- Log analysis for backend systems
- Performance profiling for optimization tasks

### When to Verify
- After each major feature block
- Before merging or deploying
- When code complexity increases
- After implementing AI suggestions you're unsure about

---

## 4. Parallel Workflows (6:53 - 8:06)

Don't crowd a single chat session with conflicting tasks.

### The Problem
- Multiple unrelated tasks create context pollution
- AI loses track of what matters for each sub-task
- Risk of mixing concerns (e.g., UI logic bleeding into data layer)

### The Solution
For large projects, **partition work into separate Claude Code sessions**. Each session gets a "clean context" for a specific sub-task.

### Example Partition Strategy
- **Session 1**: Database schema and ORM setup
- **Session 2**: API endpoint architecture and routing
- **Session 3**: Frontend component structure
- **Session 4**: Integration testing and deployment

### Benefits
- Focused problem-solving
- Reduced token overhead (no need to repeat full context)
- Easier to trace where issues originated
- Simpler to hand off work to another person

### When to Merge Sessions
Only merge back when integrating your sub-components. Each session should have clearly defined inputs and outputs.

---

## 5. Systematizing with Skills (8:06 - 9:54)

Identify your "inner loops"—tasks you perform repeatedly throughout the day.

### What Are Claude Skills?
Pre-baked plays that ensure consistency and speed without re-explaining the process each time. They're like playbooks for common tasks.

### Prompt to Identify Skills
```
Based on the project I'm working on, what Claude Skills should I create?
```

### Examples of Skills to Create
- Code review checklist (specific to your codebase)
- Testing workflow (setup, run, validate)
- Debugging protocol (capture logs, reproduce issue, isolate cause)
- Performance optimization (profile, identify bottlenecks, refactor)
- Documentation generation (extract requirements, create specs)

### How Skills Improve Over Time
- As you use them, you refine them
- They capture hard-won knowledge (edge cases, gotchas)
- New team members inherit your wisdom (consistency)
- They evolve with your codebase's needs

### Why This Beats Micro-Prompt Optimization
- Skills are reusable across projects
- They encode lessons, not just syntax
- They persist even as models improve
- They reduce cognitive load (you don't have to remember the process)

---

## 6. Build for the Future (10:00 - 11:28)

Stop obsessing over micro-prompt optimization.

### The Reality of AI Evolution
As models improve:
- Complex, highly-tuned prompts become fragile
- Simpler approaches often outperform over-engineered ones
- Time spent perfecting prompts today is partly wasted tomorrow

### Where to Invest Your Energy Instead
1. **Information Architecture**: How you structure and organize your project's context
2. **Systems & Skills**: Reusable playbooks that encode your process
3. **Feedback Loops**: Mechanisms that let you verify and course-correct
4. **Documentation**: Clear, living docs that capture intent, not just code

### The Principle
**Build for longevity, not for today's model.**

### Practical Approach
- Write clear `claude.md` (not hyper-detailed)
- Create Skills for recurring tasks
- Build verification loops into your workflow
- Document "why" decisions, not "how" to code
- Keep your codebase well-structured (AI respects good architecture)

---

## Putting It All Together: A Day in the Workflow

### Morning: Planning & Review
1. Open a **new session** for the day's main task
2. Enter **Plan Mode** (Shift + Tab twice)
3. Use the planning prompt to clarify scope
4. Update `claude.md` if needed

### Mid-Day: Build with Verification
1. Code in focused **parallel sessions** (one per sub-task)
2. Use **verification loops** to catch issues early
3. Reference **Skills** for common patterns
4. Test frequently

### End-of-Day: Consolidate & Clean
1. Merge sessions (integrate sub-tasks)
2. Run comprehensive tests
3. Clean up `claude.md` (remove clutter)
4. Document what you learned (update relevant Skills)

---

## Checklist: Am I Using This Workflow?

- [ ] **Planning**: I use Plan Mode before writing code
- [ ] **claude.md**: My system file is short, clear, and up-to-date
- [ ] **Verification**: I have a way to see the results of AI's work
- [ ] **Parallel**: I split large projects into focused sessions
- [ ] **Skills**: I've identified and created my inner-loop Skills
- [ ] **Future-Focused**: I invest in architecture, not just prompts

---

## Key Takeaway

The Claude Code workflow isn't about perfect prompting—it's about **systems that scale**.

As AI improves, your well-organized information architecture, clear Skills, and robust verification loops will continue to serve you far better than a perfectly-tuned prompt ever could.

Focus on the process. The prompts will follow.