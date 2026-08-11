# Somya Burman — Interview Prep Questionnaire & Answer Sheet

---

## SECTION 1: GENERAL / RESUME-BASED QUESTIONS

---

### Q1. Walk me through your background and how you ended up in UX design.

**Answer:**
I started as a software engineer at Capgemini, working on frontend interfaces for enterprise clients like Royal Bank of Canada using Angular and React. After two years, I realized I was more drawn to the "why" behind what I was building than the code itself. I pursued a Masters in Design at IIT Roorkee, which gave me a formal design foundation. My internship at Brew Money was my first real design role. Then I joined Enphase as an intern, working on an AR troubleshooting guide as my thesis, and was offered a full time position. I've been at Enphase for over two years now as a UX Designer 2, working across AI products, design systems, and B2B SaaS tools. I'm also pursuing a Masters in Psychology through IGNOU because understanding human cognition and behaviour directly shapes how I think about design decisions.

---

### Q2. What does your day-to-day look like at Enphase?

**Answer:**
It varies depending on which project is active. On the AI Assistant, I spend time reviewing conversation logs, looking at beta metrics (like rate, escalation patterns), identifying friction in flows, and iterating on the UI. For the design system, it's more about component architecture, token definitions, and working closely with engineering on handoff. For Solargraf, I'm often in Figma building flows for things like financing workflows, proposal editors, or dashboard visualizations. I also build internal Figma plugins when I see repetitive manual work the team shouldn't be doing.

---

### Q3. You have a CS engineering degree but moved to design. How does your engineering background help you as a designer?

**Answer:**
It helps in three specific ways. First, I understand technical constraints. When I design an AI response flow, I know what an API call looks like, what loading states mean at a system level, and where latency will show up. Second, I can prototype and build tools. I've built two Figma plugins (Dark Mode Generator, Spec & Redline Generator) and an interactive design system playbook using Windsurf and Claude. Third, I speak engineering's language during handoff. I can articulate spacing in tokens, describe component states precisely, and debug implementation mismatches without needing a translator.

---

### Q4. Why are you pursuing a Masters in Psychology alongside your design work?

**Answer:**
Design decisions are fundamentally about predicting human behaviour. Psychology gives me a structured framework for that. Understanding concepts like cognitive load, decision fatigue, and environmental context change directly influences how I design. For example, in the AI Assistant, the icon and color swap during agent handoff leverages a cognitive psychology principle: environmental context change signals a mode switch. That's not something I would have thought of purely from a visual design perspective.

---

### Q5. Tell me about a time you failed or something didn't go as planned.

**Answer:**
The first version of the AI Assistant (V1) was essentially a failure we had to learn from. It was built on a Salesforce shell with if/else branching logic instead of a real LLM. Conversations felt rigid, like an IVR menu. The UI was constrained by the Salesforce design system because we chose developer speed over design flexibility. Within weeks, it was clear the whole approach was wrong. We had to rebuild from scratch for V2. The lesson was that taking shortcuts on the interaction model (branching logic vs. real conversational AI) created more rework than building it right the first time. The rebuild took longer, but V2 scaled across 4 platforms and is now live in production with 229K users.

---

## SECTION 2: ENPHASE AI ASSISTANT (Primary Case Study)

---

### Q6. Walk me through the Enphase AI Assistant project from start to finish.

**Answer:**
We started by analyzing 3,500 support calls across Q3-Q4 2023. The data showed the top 30% of call volume was dominated by repetitive queries: site status checks (11.9%), gateway connectivity (9.9%), battery issues (4.8%) for homeowners, and microinverter PLC issues (8.27%), site checks (6.8%), WiFi problems (4.9%) for installers. About 60% of these were automatable.

The average wait time was 7.1 minutes per call, and average time on call was 22 minutes. 15-18% were repeat calls just asking for status updates on open cases.

We also ran qualitative interviews with homeowners, installers, and CS agents. Homeowners were scared by error messages. Installers needed quick answers on-site. CS agents spent the first 5-10 minutes of every call just pulling up information.

From there, I designed one unified AI layer serving three personas (homeowner, installer, support agent) across four ingress points (Homeowner App, ITK installer app, Enlighten Manager, Enphase website). Each persona gets adapted tone, depth, and response format.

I grounded the design in Microsoft's 18 AI Design Guidelines, applying 7 key principles: graceful escalation, transparent loading states, context-aware presets, capability communication, non-blocking responses, persona-adaptive tone, and feedback with fallback menus.

The visual design established yellow as the AI identity color, used native app colors for tappable text to respect learned affordances, and implemented icon + color swaps on agent handoff.

For handling system complexity, I mapped four foundational patterns: API data fetching, task automation, restricted access with secure redirection, and step-by-step guided troubleshooting.

Beta was released to 50K initially and expanded to 229K. Results: 95.3K messages exchanged, 49.8K sessions, 87.35% like rate, less than 1% escalation to human agents, 3,806 likes vs 552 dislikes.

---

### Q7. How did you decide which problems the AI should solve first?

**Answer:**
Data driven prioritization. We analyzed 3,500 support calls and categorized them by volume and impact. The top 30% of homeowner calls were site status checks (11.9%), gateway connectivity (9.9%), battery issues (4.8%), and system access (3.3%). For installers, it was microinverter PLC issues (8.27%), site checks (6.8%), network/WiFi (4.9%), gateway replacement (4.85%), and stuck booting (4.67%). We focused on the highest volume, highest automatable queries first. About 60% of total call volume was automatable via AI.

---

### Q8. How did you design for three completely different personas in one AI system?

**Answer:**
The key insight was that the AI layer is the same, but the presentation adapts. When launched from the Homeowner App, the assistant picks up the persona automatically and uses simple, empathetic, jargon-free language. From the installer app (ITK), it switches to direct, technical, no-fluff responses with device telemetry and diagnostics context. For support agents on Enlighten Manager, it provides structured, context-rich, actionable information with ticket history and fleet data.

The preset menus also adapt. Homeowners see "Why is my bill high?" and "Check battery status." Installers see "Run commissioning check" and "Gateway LED troubleshooting." This context awareness means users don't start from a blank prompt.

On the website, where persona isn't known, the assistant asks who you are first, then tailors the experience.

---

### Q9. Tell me about a specific design decision you iterated on and why.

**Answer:**
The preset menu discoverability issue during alpha testing. The preset menu (quick action options) only appeared on first launch and disappeared once a conversation started. Users kept asking how to get back to those options without exiting and reopening the assistant. The fix was moving the menu to a persistent, always accessible location in the fixed menu bar.

Another example: feedback and utility actions (thumbs up/down, read aloud, copy) were hidden behind a three-dot overflow menu. Usage was extremely low. Since this was a new product and we needed feedback data to train and improve the models, burying these controls was actively working against us. We surfaced them directly under every response. This was a case where product needs (collecting training data) and user needs (easy feedback) aligned, and the design was blocking both.

---

### Q10. What was the hardest design challenge on the AI Assistant?

**Answer:**
Designing for ambiguity at scale. The Enphase ecosystem isn't one product. It spans homeowner apps, installer tools, fleet management dashboards, support portals, and the public website. A homeowner asking "why is my bill high?" and an installer debugging a gateway communication fault are fundamentally different problems, but both land in the same AI assistant.

I had to map four foundational patterns to handle this: direct API data fetching for straightforward queries, task automation for actions like restarting a device, restricted access with secure redirection for sensitive operations like billing, and step-by-step guided troubleshooting for multi-step technical processes. Each pattern has different UI flows, confirmation requirements, and fallback behaviors.

---

### Q11. How did you handle the transition from AI to human support agent?

**Answer:**
This was a deliberate design decision informed by cognitive psychology. When the AI transfers to a human agent, two things change simultaneously: the assistant icon swaps to an agent icon, and the chat theme shifts from yellow (AI identity color) to the native app color. This double signal, visual identity plus color environment, makes the transition unmistakable. Users don't need to read a system message to know they're talking to a real person.

The principle behind it: environmental context change signals a mode switch, reducing the chance of users treating agent responses as AI-generated. This matters because trust dynamics are different when talking to a human versus an AI.

---

### Q12. Why did you use Microsoft's AI Design Guidelines? Did you consider other frameworks?

**Answer:**
Microsoft's 18 AI Design Guidelines were the most practical and comprehensive framework available for conversational AI at the time. They covered the exact tensions we were dealing with: capability communication, graceful degradation, transparency, and fairness across personas.

I didn't apply all 18 blindly. I mapped the 7 most critical ones to our context: graceful escalation, transparent thinking states, context-aware presets, capability communication, non-blocking responses, equitable persona-adaptive tone, and feedback with fallback menus. Each principle was adapted specifically to Enphase's context of solar energy, where users range from anxious homeowners to time-pressured installers.

Having a structured framework also helped during stakeholder conversations. Instead of debating subjective design preferences, I could point to established principles and explain why a specific decision was made.

---

### Q13. What does "less than 1% escalation rate" actually mean, and why does it matter?

**Answer:**
It means that out of all conversations the AI handled, fewer than 1% resulted in the user being transferred to a human support agent because the AI couldn't resolve the issue. Out of 95.3K messages, 831 chats were escalated.

This matters for two reasons. First, it validates that the AI is actually solving problems, not just deflecting them. Second, it's a direct cost metric. Every escalation means a human agent's time. At the previous average of 22 minutes per call, keeping escalation under 1% represents significant operational savings. But the 831 escalated chats were also valuable. They revealed edge cases where AI confidence was high but accuracy was low, which fed directly into model improvement.

---

### Q14. The like rate is 87.35%. What about the remaining 12.65%?

**Answer:**
552 explicit dislikes out of 4,358 total feedback responses. But most users who weren't satisfied simply didn't leave feedback at all, so the dislike number is a floor, not a ceiling. The dislikes were valuable because they pointed to specific failure modes: incorrect technical information about specific hardware models, overly generic answers for installer-specific queries, and cases where the AI was confident but wrong.

We used this feedback loop to identify patterns. If a specific type of query consistently got dislikes, it flagged a gap in the agent's knowledge base or a prompt engineering issue. This was one reason we fought to surface the feedback buttons directly under every response instead of hiding them behind an overflow menu.

---

### Q15. How did you measure success for this project?

**Answer:**
Quantitative: 95.3K messages exchanged, 49.8K sessions, 229.3K beta users, 87.35% like rate, less than 1% escalation rate, 3,806 likes received.

Qualitative: The assistant is live in production across all four platforms. It's serving real customers daily. The YouTube walkthrough of the production implementation demonstrates it's not a prototype or concept.

Operational: Reduction in support call volume for automatable queries. The 60% of call volume that was identified as automatable is now being handled by the AI.

---

### Q16. You mentioned "70+ specialized agents." What does that mean and how did it affect your design?

**Answer:**
The AI isn't a single model. It uses Claude and Gemini as base models, but 70+ specialized agents handle specific domains: battery diagnostics, gateway troubleshooting, energy billing explanations, installation commissioning, etc. Each agent is grounded in real-time Enlighten data.

For design, this meant I had to design the loading and thinking states to reflect what was actually happening. Instead of a generic spinner, users see multi-stage indicators like "Analyzing your image...", "Fetching system data...", "Preparing insights..." Each query type has its own sequence of thinking states. This transparency builds trust because users understand the system is doing real work, not just generating text.

---

## SECTION 3: SOLARIS 2.0 DESIGN SYSTEM

---

### Q17. Walk me through the Solaris 2.0 Design System project.

**Answer:**
Solargraf's existing design system had no token architecture. Colors were hard-coded, spacings were arbitrary (12px here, 14px there), radii were inconsistent (8px on buttons, 10px on cards, 12px on modals), and there were 12+ shades of grey with no naming convention. Designers detached components constantly because nothing had auto-layout or configurable width.

My contribution started with an audit. I cataloged every inconsistency: the greys, the spacing drift, the radius mismatches, the typography with no shared scale. Then I designed a two-tier token architecture: raw tokens hold primitive values (grey-500, spacing-8) and semantic tokens reference them with meaning (text-secondary, surface-mainAction). This separation allows context updates without touching components and enables future theme switching.

I built 10+ components across three levels: 4 atoms (button, input field, badge, toggle), 5 molecules (form group, dropdown, search bar, stat card, toast), and 1 organism (data table with sortable columns, pagination, row actions, bulk select). The most complex piece was the Input Card Form, rebuilt with a slot-based architecture where designers swap content without detaching.

The project had two outcomes: a Figma design system library and an interactive developer playbook built with Windsurf and Claude Opus, featuring live component variants in the browser, copy-ready code snippets, and visual prop controls.

Timeline was 4 months with a team of 2 designers. Impact: 10+ components built, 80+ semantic tokens defined, and an estimated 30% faster design handoff.

---

### Q18. Explain your two-tier token architecture. Why two tiers instead of one?

**Answer:**
Raw tokens are the primitive values: grey-500 is #808080, spacing-8 is 8px. Semantic tokens reference raw tokens but carry meaning: text-secondary maps to grey-500, surface-mainAction maps to BrandBlue400.

Two tiers matter because they decouple "what color is this" from "what does this color mean." If the brand blue changes from #2382c4 to something else, I update one raw token and every semantic token referencing it updates automatically. If I want to change what "disabled" looks like, I change the semantic mapping without touching the raw values.

This also enables theme switching. A dark mode would only need new semantic mappings, not new components. And it creates a shared language between design and engineering. Engineers don't reference hex values. They reference text-secondary or surface-mainAction, which makes the code self-documenting.

---

### Q19. Tell me about the slot-based architecture for the Input Card Form.

**Answer:**
The Input Card Form was the most-used pattern in Solargraf. Previously, designers detached it every single time because it couldn't accommodate different content. I rebuilt it with a Card shell that has named content slots: Title, Content, and Slots (for form inputs). Designers swap the content inside each slot without ever detaching the component.

The Figma implementation uses component properties and auto-layout so the card adapts to any width and content configuration. The same Card component can hold a text input form, a checkbox group, a date picker setup, or a dropdown configuration, all without breaking the master component. This eliminated the primary reason designers were detaching components.

---

### Q20. You built an interactive playbook with Windsurf and Claude. Why not just Storybook or a Figma-based handoff?

**Answer:**
The playbook was specifically designed to bridge the gap for a team that didn't have Storybook set up yet. It provides live component variants that developers can interact with in the browser, toggle states, change sizes, and see the visual output immediately. Copy-ready code snippets sit next to each variant.

I built it using Windsurf (AI-assisted IDE) and Claude Opus because the goal was speed and self-containment. The output is a single HTML file with inline CSS and JavaScript, no build system, no dependencies. Developers open it in a browser and it just works. It's not a replacement for Storybook, but it filled an immediate need while the engineering team evaluates their tooling.

---

## SECTION 4: SOLARGRAF ICON SET

---

### Q21. Walk me through the icon redesign project.

**Answer:**
Solargraf's icons were sourced from multiple libraries with varying styles, weights, and visual logic. The same icon was reused for "Project" and "View Company." Stroke weights mixed 1px, 1.5px, and 2px within the same view. Corner radii were inconsistent, and there was no optical size compensation.

As the sole designer on this initiative, I started by defining a strict 10-rule checklist before drawing anything: 24x24px grid, 18px optical safe zone, 1px stroke weight, whole number element sizes (preferably even), center-aligned strokes, minimum 1px gap between elements, 1px shape cuts, no corner radius unless the shape demands it, rounded corner joins and stroke caps, and additional elements positioned at bottom-right.

I followed a four-phase process: audit, ideation and exploration, refinement and testing (at minimum and maximum sizes), and library handoff. The final output was 40+ icons across 4 product areas, organized in a Figma component library with search-friendly naming, size variants, and usage documentation.

---

### Q22. Why was inconsistent iconography more than just a visual problem?

**Answer:**
The inconsistency was cognitive. Users were learning different visual languages in different parts of the same product. When the "Project" icon and the "View Company" icon are the same, users can't build reliable mental models of what icons mean. When stroke weights shift between views, the visual hierarchy breaks. Icons that look different sizes (due to no optical compensation) create a perception that some features are more important than others, unintentionally.

All of this adds up to unnecessary cognitive load. Every time a user has to think "wait, what does this icon mean?" or "is this the same as that other screen?" they're spending mental energy on the interface instead of their actual task (designing solar systems, creating proposals).

---

### Q23. How did you decide on the design rules (1px stroke, 24px grid, etc.)?

**Answer:**
The 24x24px grid with 18px optical safe zone is an industry standard that ensures icons remain legible at small sizes while leaving breathing room. I chose 1px stroke weight because Solargraf's UI is information-dense, and thinner strokes reduce visual noise without sacrificing clarity. Heavier strokes would compete with the data-heavy content.

Rounded joins and stroke caps were chosen to create a softer, more approachable feel that aligned with Solargraf's brand positioning. The "no corner radius unless shape demands it" rule prevents the inconsistency that plagued the old set, where some icons had sharp corners and others were fully rounded.

The "even numbers" rule for element sizes prevents sub-pixel rendering issues. The 1px minimum gap prevents visual merging at small sizes. Each rule exists to solve a specific problem we observed in the audit.

---

## SECTION 5: AR SELF-TROUBLESHOOTING GUIDE (M.Des Thesis)

---

### Q24. Tell me about your AR troubleshooting guide thesis project.

**Answer:**
This was my M.Des thesis at IIT Roorkee, done during my internship at Enphase. The problem: homeowners with solar systems had to call customer support for issues they could potentially resolve themselves, like power cycling batteries. Average resolution time was 30-40 minutes, mostly waiting on hold.

I followed a double diamond design approach. In the discovery phase, I interviewed homeowners, customer support agents, and installers. Key insights: homeowners were scared of error messages, didn't want to guess on fixes, and most issues had a hardware component that could be guided visually. CS agents said 30% of issues could be self-resolved with proper guidance.

The solution was an AR-based guide within the Enphase Homeowner App that lets users point their camera at their solar equipment and receive step-by-step visual guidance overlaid on the physical device. The approach included in-app troubleshooting, visual guides, AR guidance, and sticker sheets for physical devices.

Estimated impact: 50,400+ support calls reduced per year, 25,200+ CS hours saved, and 15,120+ homeowners empowered to self-resolve. It received an Honourable Mention at Enphase's Ennovate'23 innovation contest (130+ global entries).

---

### Q25. How did you validate the AR approach over other solutions?

**Answer:**
I studied existing first-contact resolution channels: blogs and articles (too generic, not context-specific), online communities (inconsistent advice, delayed responses), and product manuals (too technical, hard to follow physically). All of these fail at the critical moment when a homeowner is standing in front of their equipment, stressed, and needs to do something physical.

AR solves this because it overlays guidance directly onto the physical device. The user doesn't have to translate written instructions into physical actions. They see exactly which button to press, which cable to check, which LED to look at. This reduces error rate and builds confidence. The 30% of issues that CS agents identified as self-resolvable were primarily hardware interaction tasks, exactly the type of task where spatial, visual guidance outperforms text.

---

## SECTION 6: FIGMA PLUGINS (Dark Mode Generator & Spec/Redline Generator)

---

### Q26. Tell me about the Figma plugins you built.

**Answer:**
I built two plugins to solve team productivity problems:

**Color Theme Changer (Dark Mode Generator):** For design systems without token-based theming, this plugin uses AI-assisted semantic color interpretation to automatically transform light themes to dark themes. It maps colors based on their meaning (background, surface, text, etc.) rather than just inverting values. Built with Windsurf and Figma Plugin API, using prompt engineering for the color mapping logic.

**Spec & Annotation Generator:** This automates developer handoff by generating spacing specs, layout redlines, and interface annotations from selected Figma frames. Instead of manually measuring and annotating every element (which designers were spending significant time on), the plugin auto-generates the annotations. This reduced manual QA and handoff prep time across the team.

Both were born from observing repetitive manual work. I saw designers spending hours on tasks that could be automated, and my engineering background meant I could actually build the solution.

---

## SECTION 7: DESIGN THINKING & PROCESS QUESTIONS

---

### Q27. How do you approach a new design problem?

**Answer:**
I start with data, not sketches. On the AI Assistant, the first thing I did was analyze 3,500 support calls. On the icon set, I started with a visual audit. On Solaris, I cataloged every inconsistency before defining a single token.

Then I define constraints and principles before solutions. For icons, that was the 10-rule checklist. For the AI assistant, it was the 7 AI design guidelines. For the design system, it was the two-tier token architecture.

I prototype and test early. During alpha testing of the AI assistant, we caught the preset menu discoverability issue before it reached 229K beta users. The icon set was tested at minimum and maximum sizes before finalizing.

And I use feedback loops aggressively. The AI assistant has thumbs up/down on every response. The beta data (95.3K messages, 87.35% like rate, 831 escalations) directly informed post-beta design decisions.

---

### Q28. How do you work with engineers?

**Answer:**
Three specific practices. First, I speak their language. Token names like text-secondary and surface-mainAction are self-documenting in code. The interactive playbook gives them copy-ready snippets. The Figma plugins I built demonstrate I understand their workflow.

Second, I design for implementation reality. When I designed the AI thinking states, I mapped them to actual backend processes (fetching data, analyzing images, preparing insights) rather than inventing arbitrary loading animations.

Third, I reduce handoff friction through tooling. The Spec & Annotation Generator plugin automated the most tedious part of design-to-dev handoff. The slot-based component architecture means engineers implement one Card component, not dozens of card variants.

---

### Q29. How do you prioritize when you have multiple projects running?

**Answer:**
At Enphase, I'm typically running 2-3 projects simultaneously. I prioritize based on user impact and urgency. The AI Assistant takes priority when there's live beta data showing friction (like the preset menu issue). The design system takes priority when multiple teams are blocked by component gaps. Icon work and plugin development happen in focused sprints between major milestones.

I also think about what unblocks others. If three developers are waiting for a component spec, that gets priority over a visual polish task on a different project. If the AI team needs design decisions to ship a feature, that moves up.

---

### Q30. How do you handle disagreements with stakeholders or PMs?

**Answer:**
I lead with data. On the AI Assistant, when the question came up about whether to surface or hide feedback buttons, I pointed to the usage data showing almost no engagement with the overflow menu. That made it a data conversation, not a taste conversation.

On the threads bar removal during beta, it wasn't my opinion that threads weren't useful. It was the data: fewer than 8% of sessions used the "New chat" button, and thread switching accounted for less than 3% of interactions. Users were in a hurry to resolve issues, not organize chat history. The data made the decision obvious.

When data isn't available, I prototype both options and test with users. I'd rather spend a day building two prototypes than a week debating hypotheticals.

---

## SECTION 8: BEHAVIORAL & SITUATIONAL QUESTIONS

---

### Q31. Tell me about a time you had to design something from 0 to 1.

**Answer:**
The V2 rebuild of the AI Assistant. V1 was a Salesforce shell with branching logic. V2 was designed from scratch to work across 4 platforms, 3 personas, with real LLM integration. I defined the entire information architecture: how the assistant detects persona from the launching app, how preset menus adapt to context, how conversation threads work, how the handoff to human agents looks and feels, how the visual identity (yellow) stays consistent while respecting each platform's native color language. There was no existing pattern to follow because no other solar company had built something like this.

---

### Q32. Describe a project where you had to balance speed with quality.

**Answer:**
The Solaris 2.0 playbook. The engineering team needed component documentation immediately, but building a full Storybook integration would have taken weeks. I used Windsurf and Claude Opus to build a self-contained HTML playbook in days. It's not as polished as a production Storybook, but it gives developers live interactive components, prop controls, and copy-ready code right now. The tradeoff was explicit: ship something useful fast and iterate toward the ideal solution. The team was unblocked within the week.

---

### Q33. How do you handle designing for accessibility in your work?

**Answer:**
In the AI Assistant, accessibility shows up in several ways. The feedback mechanism is always visible (not hidden behind menus). Loading states are multi-stage text descriptions, not just visual spinners, so screen readers can communicate progress. The color system uses yellow (#ffcc00) as the AI identity, which was chosen for its high visibility and contrast against dark backgrounds.

In the design system, every component ships with all interaction states: default, focus, error, success, and disabled. This ensures keyboard navigation and assistive technology can identify component states. The semantic token architecture also helps because tokens like text-secondary carry meaning that can be mapped to ARIA roles in implementation.

For icons, the 18px optical safe zone within the 24px grid ensures legibility at small sizes, and the consistent 1px stroke weight maintains visual clarity across screen densities.

---

### Q34. What's a design trend you disagree with?

**Answer:**
The tendency to hide complexity behind "clean" interfaces. In enterprise tools like Solargraf, users are professionals who need data density. Removing information to make things look minimal actually slows them down because they have to click through more screens to find what they need. Good enterprise design isn't about removing information. It's about organizing it so the right information is findable at the right time. The slot-based Card component I built for Solaris is an example: it looks clean but can hold dense form layouts without visual chaos.

---

### Q35. Where do you see your career going in the next 3-5 years?

**Answer:**
I want to go deeper into AI-native product design. Not just adding AI features to existing products, but designing products where AI is the core interaction model. My psychology studies are building toward this: understanding how people form trust with AI systems, how conversation patterns differ from GUI patterns, and how to design for the gap between AI confidence and AI accuracy.

I'm also interested in the intersection of design systems and AI. Imagine a design system that adapts its components based on user behaviour data, or tools that help designers make evidence-based decisions about component variants. That's the direction I find most exciting.

---

## SECTION 9: PORTFOLIO-SPECIFIC DEEP DIVE QUESTIONS

---

### Q36. Your portfolio shows both B2C (homeowner app) and B2B (Solargraf, installer tools). How does your approach differ?

**Answer:**
B2C (homeowner): Emotional design matters more. Homeowners are scared of error messages, confused by technical jargon, and anxious about their energy bills. The AI Assistant uses empathetic, simple language. Visual cues need to build confidence. Error states need to reassure, not alarm.

B2B (Solargraf, installer tools): Efficiency is the priority. Installers are on-site, time-pressured, and technically fluent. They want direct, no-fluff answers. The same AI assistant switches to technical language, shows device telemetry, and skips the hand-holding. In Solargraf, the design tool and proposal editor were restructured around speed, cutting average proposal edit time by approximately 40% with the Express Editor.

The shared thread is that both need clarity. A homeowner needs clarity about what their system is doing. An installer needs clarity about what's broken and how to fix it. The information architecture changes, but the principle of "reduce time to understanding" stays constant.

---

### Q37. You redesigned the Solargraf proposal flow and cut edit time by 40%. How?

**Answer:**
I restructured the feature hierarchy into primary, secondary, and tertiary tiers. Previously, all features had equal visual weight, which meant users had to scan everything to find the one thing they needed. By tiering the features, the core workflow (the actions users do on every proposal) became faster to access. The Express Editor Tool was the implementation of this: it surfaced the most common editing actions while pushing rarely-used options behind progressive disclosure. The 40% reduction came from fewer clicks, less scanning, and a clearer path through the editing flow.

---

### Q38. You designed multi-lender financing workflows. What was challenging about that?

**Answer:**
Supporting 5 lending partners meant 5 different data schemas, different qualification criteria, different rate structures, and different user flows. The challenge was creating a unified comparison experience where installers could evaluate options side by side without the UI becoming a spreadsheet.

I had to balance showing enough detail for informed decisions (rates, terms, qualification requirements) while keeping the flow integrated within the proposal experience rather than being a separate standalone tool. The design had to handle cases where a homeowner qualifies for some lenders but not others, which required clear status communication without making the rejected options feel like failures.

---

### Q39. What's the India Runs on Chai project about and why is it in your portfolio?

**Answer:**
It's a personal data visualization project. I surveyed people about their chai habits and turned the data into illustrated infographics with a folk art style. 49% of respondents drink chai just for comfort. I mapped 3 distinct chai personas based on consumption patterns.

It's in my portfolio because it shows a different side of my skillset: illustration, data visualization, and personal project initiative. It demonstrates that I can communicate data through storytelling and visual narrative, not just dashboards and UI. For a design portfolio, showing range matters. It also shows I'm curious beyond my day job.

---

### Q40. If you could redo one of your projects from scratch, which would it be and what would you change?

**Answer:**
The Solaris 2.0 design system. I would push harder for the full token architecture from day one instead of building 10+ components first. In hindsight, the token system should have been the first deliverable, fully documented and adopted by engineering, before a single component was built. That way, every component would have been token-native from its first version. We ended up with some retrofitting that could have been avoided.

I'd also advocate for integrating the playbook into the engineering CI/CD pipeline earlier, so component documentation stays in sync with code automatically rather than being a separate artifact that needs manual updates.

---

## SECTION 10: RAPID FIRE / CURVEBALL QUESTIONS

---

### Q41. What's your design tool stack?

**Answer:** Figma (primary), FigJam (workshops and brainstorming), Adobe Illustrator (icon work and illustration), Jira (project tracking), Claude (AI-assisted design thinking and content), Windsurf and Cursor (AI-assisted development for plugins and playbooks).

### Q42. How do you stay updated on design trends and AI developments?

**Answer:** I'm actively building with AI tools (Windsurf, Claude, Cursor), which keeps me closer to the technology than reading about it. My psychology coursework exposes me to research on cognition and behaviour that directly applies to AI interaction design. I also learn by doing: building Figma plugins, creating the interactive playbook, and working with real LLM outputs daily.

### Q43. What's one thing you'd improve about Figma?

**Answer:** Native support for design tokens with semantic layers. Figma's variables are a step in the right direction, but managing a two-tier token system (raw and semantic) still requires workarounds. If Figma had native raw-to-semantic mapping with named contexts, design systems like Solaris would be significantly easier to maintain.

### Q44. How do you handle design critique?

**Answer:** I separate the work from my identity. Critique is about the design, not about me. I also try to present work with clear rationale so critique is grounded in "does this decision achieve the goal" rather than subjective preference. When I get feedback I disagree with, I ask for the reasoning. Sometimes that changes my mind. Sometimes it surfaces a constraint I didn't know about. Sometimes I push back with data.

### Q45. What makes a great design system?

**Answer:** Three things. First, adoption: if designers aren't using it, it doesn't matter how elegant the token architecture is. Second, zero-detach rate: components should be flexible enough that nobody ever needs to detach them. Third, a shared language: when a designer says "surface-mainAction" and an engineer knows exactly what that means in code, the system is working. The playbook and tokens I built for Solaris were designed around all three.

---

---

## SECTION 11: UX RESEARCH METHODS I USED

---

### Q46. What UX research methods did you use across your projects?

**Answer:**

**Quantitative methods:**

- **Support call log analysis (AI Assistant):** Analyzed 3,500 support calls across Q3-Q4 2023. Categorized by volume, issue type, and automation potential. This gave us the top 30% of call volume breakdown and the 60% automatable figure.
- **Beta analytics tracking (AI Assistant):** Tracked 229K+ users across 49.8K sessions and 95.3K messages. Measured session counts, message volume, like/dislike rates, escalation rates, thread switching frequency, and new chat button usage.
- **In-product feedback collection (AI Assistant):** Thumbs up/down on every AI response. 4,358 total feedback responses (3,806 likes, 552 dislikes). Used this to calculate the 87.35% like rate and identify failure patterns.
- **Feature usage analytics (AI Assistant beta):** Tracked specific UI interactions like thread switching (less than 3% of interactions) and new chat button usage (less than 8% of sessions) to inform the threads bar removal decision.
- **Visual audit and inventory (Solaris 2.0, Icon Set):** Cataloged every inconsistency: 12+ shades of grey with no naming convention, mixed stroke weights (1px, 1.5px, 2px), inconsistent radii (8px, 10px, 12px), arbitrary spacings (12px, 14px). This was quantitative evidence that justified the redesign.

**Qualitative methods:**

- **Stakeholder interviews and discussion sessions (AI Assistant):** Conversations with three user groups: homeowners, installers, and CS agents. These were semi-structured discussions focused on frustrations, workarounds, and unmet needs. Produced the six core user quotes that shaped the design direction.
- **Contextual inquiry (AI Assistant, AR Guide):** Observed CS agents during live calls to understand their workflow. Discovered the 5-10 minute information gathering phase at the start of every call. For AR, observed homeowners interacting with their physical solar equipment.
- **Competitive and analogous research / desk study (AI Assistant):** Studied existing first-contact resolution channels: blogs, online communities, product manuals, and existing chatbot implementations. Identified why each failed at the critical moment of need.
- **Alpha testing with internal users (AI Assistant):** Released V2 to a controlled group before wider beta. Collected qualitative feedback on design direction and LLM response quality. Surfaced two specific friction points (preset menu discoverability, hidden feedback actions).
- **Double diamond process (AR Guide thesis):** Full discovery and definition phases with interviews across homeowners, CS agents, and installers during the M.Des thesis at IIT Roorkee.
- **Design system audit (Solaris 2.0):** Systematic review of every component, token, and pattern in the existing Solargraf design system to identify detachment patterns, naming inconsistencies, and architectural gaps.

---

### Q47. How did you decide which research method to use for each project?

**Answer:**
It depends on what question I'm trying to answer. If the question is "how big is this problem," I reach for quantitative data. The 3,500 call log analysis answered "what are people calling about" at scale. If the question is "why does this happen," I talk to people. The stakeholder discussions revealed that homeowners were scared of error messages, something no call log would tell you.

For the AI Assistant, I layered both. Quantitative data (call volumes, wait times) told us what to build. Qualitative data (user quotes, agent observations) told us how to build it. During beta, the in-product analytics told us what was working at scale, and the feedback comments told us what was failing in specific cases.

For the design system, the audit was the right tool because the problem was inconsistency, which you can count and catalog. For icons, the same: visual audit first, then testing at minimum and maximum sizes to validate the design rules.

---

## SECTION 12: QUESTIONS I ASKED USERS DURING DESIGN AND TESTING

---

### Q48. What kinds of questions did you ask during the discovery phase?

**Answer:**

**Questions for homeowners:**
- What happens when you see an error message on your system? What do you do first?
- When was the last time you called Enphase support? What was it about?
- If you could check one thing about your solar system without calling anyone, what would it be?
- How do you feel about troubleshooting electrical equipment on your own?
- What would make you trust an AI assistant to give you accurate information about your home energy system?

**Questions for installers:**
- Walk me through your last on-site installation. Where did you get stuck or need help?
- When you call installer support, what information do you already have and what do you need them to look up?
- How do you tell the difference between a hardware fault and a provisioning issue on site?
- If you had an assistant on your phone during a job, what would you ask it first?
- What's the most time consuming part of commissioning a new system?

**Questions for CS agents:**
- Walk me through the first five minutes of a typical inbound call. What do you do before you start solving the problem?
- What percentage of your calls do you think the customer could have resolved without you?
- What information do you wish you had before the customer even connected?
- How do you decide when an issue is urgent versus routine?
- What are the most common things customers call back about?

The goal with all of these was to understand behaviour and workarounds, not just stated preferences. The homeowner who said "I get scared when I see an error" told us more about the design direction than any feature request would have.

---

### Q49. What questions did you ask during alpha and beta testing?

**Answer:**

**Alpha testing (qualitative, controlled group):**
- Can you find the preset menu options after starting a conversation? (This directly surfaced the discoverability issue.)
- When the AI gives you a response, what do you do next? Do you notice anything you can interact with below the response?
- Does the AI feel like it understands your question? If not, what happened?
- When the AI transferred you to a human agent, was the transition clear? Did you know you were talking to a person?
- Is there anything you tried to do that the assistant couldn't help with?

**Beta testing (quantitative at scale, 229K users):**
We didn't ask questions directly during beta. Instead, we instrumented the product to answer questions through behaviour data:
- Are users starting new conversations or continuing existing ones? (Answered by new chat button usage: less than 8%)
- Are users switching between conversation threads? (Answered by thread interaction rate: less than 3%)
- Are users satisfied with AI responses? (Answered by like/dislike ratio: 87.35% like rate)
- Where does the AI fail? (Answered by escalation tracking: 831 escalated chats out of 95K+ messages)
- Which response types get the most dislikes? (Used to identify gaps in specific agent knowledge bases)

The shift from alpha to beta was a shift from "ask users what they think" to "watch what users actually do." Both are necessary, but they answer different questions.

---

### Q50. What questions did you ask when designing specific workflows and interaction patterns?

**Answer:**

**When designing the escalation flow:**
- At what point should the AI stop trying and connect the user to a human? (Answered through confidence thresholds and repeated misunderstanding detection.)
- How should the transition feel? Should it be abrupt or gradual? (Led to the icon swap + color change double signal.)

**When designing preset menus:**
- What are the top 5 things each persona asks about? (Derived from the call log analysis.)
- Should presets be static or adapt to context like active alerts and recent activity?
- When in the conversation should presets be available? (Alpha feedback answered this: always, not just on first launch.)

**When designing the four complexity patterns:**
- For each user query type, what's the simplest path to resolution?
- Does this action require user confirmation before executing? (Yes for task automation like device restart. No for data fetching.)
- Does this action involve sensitive data that needs higher authentication? (Led to the restricted access pattern with secure redirection.)
- Can this be resolved in one step or does it need a guided multi-step flow? (Led to the step-by-step troubleshooting pattern.)

**When designing for the design system (Solaris 2.0):**
- Why are designers detaching this component? What content doesn't fit?
- What's the minimum set of props that makes this component flexible enough to never detach?
- Can an engineer read this token name and know exactly what it controls without looking at the Figma file?

---

## SECTION 13: HOW I MEASURED IMPACT METRICS

---

### Q51. How did you measure the impact metrics in your case studies? Walk me through each one.

**Answer:**

**AI Assistant metrics:**

- **229.3K beta users:** Total count of unique users enrolled in the beta pilot. This was a product analytics number pulled from the backend. Started at 50K initially and expanded as the beta progressed.
- **95.3K messages exchanged:** Total message count (both user messages and AI responses) tracked through the conversation backend. Every message was logged with a timestamp, session ID, user persona, and platform.
- **49.8K sessions:** A session was defined as a continuous interaction from opening the assistant to closing it or timing out. Tracked via session IDs in the analytics pipeline.
- **87.35% like rate:** Calculated as likes / (likes + dislikes). 3,806 likes out of 4,358 total feedback responses. This only counts users who actively gave feedback, not all users. Most users who were unsatisfied simply didn't leave feedback, so the dislike number is a floor, not a ceiling.
- **Less than 1% escalation rate:** 831 escalated chats out of 95.3K+ total messages. An escalation was triggered when the AI detected low confidence, repeated misunderstanding, or the user explicitly requested a human agent. Each escalation was logged with the conversation context.
- **3,806 likes / 552 dislikes:** Raw count from the in-product thumbs up/down mechanism. Every AI response had visible feedback buttons (surfaced after the alpha fix). Dislikes were tagged with the query type to identify failure patterns.
- **Thread switching less than 3%, new chat less than 8%:** Tracked via interaction events on the threads bar and new chat button. These were standard product analytics events measured over the full beta period across 229K users.

**How we used these metrics:**
The like/dislike data wasn't just a scorecard. We used the 552 dislikes to identify specific failure modes: incorrect technical info about hardware models, overly generic answers for installer queries, and cases where the AI was confident but wrong. Each dislike pattern flagged a gap in the agent's knowledge base or a prompt engineering issue.

The escalation data (831 chats) was similarly diagnostic. We analyzed escalated conversations to understand what types of queries the AI couldn't handle and used that to prioritize model improvement.

**Solaris 2.0 Design System metrics:**

- **10+ components built:** Direct count of atoms (4), molecules (5), and organisms (1) delivered in the Figma library.
- **80+ semantic tokens defined:** Count of tokens in the two-tier architecture. Each token was documented with its raw value reference, semantic meaning, and usage context.
- **30% faster design handoff (estimated):** This was an estimated projection based on the reduction in steps required. Before: designers detached components, manually adjusted values, wrote separate specs. After: components work without detaching, tokens carry meaning into code, the playbook provides copy-ready snippets. The 30% estimate came from comparing the number of manual steps eliminated. It wasn't measured with a stopwatch because the system was still being adopted.

**Icon Set metrics:**

- **40+ icons across 4 product areas:** Direct count of icons delivered.
- **Testing at minimum and maximum sizes:** Each icon was rendered at its smallest usage size (16px) and largest (48px) to verify legibility and visual consistency. This was a manual QA process, not automated testing.

**AR Troubleshooting Guide metrics:**

- **50,400+ support calls reduced per year (estimated):** Based on the CS agent insight that 30% of issues could be self-resolved with proper guidance. Applied to the annual call volume for the target issue categories.
- **25,200+ CS hours saved (estimated):** Derived from the reduced call count multiplied by average call duration (22 min + 7.1 min wait time).
- **15,120+ homeowners empowered (estimated):** Count of unique homeowners who would benefit from self-service resolution annually, based on the repeat caller data (15-18% of calls were repeat calls for status updates).

These were projections, not measured actuals, because the AR guide was a thesis project that received an Honourable Mention at Enphase's Ennovate'23 contest but was not fully deployed at the time.

---

### Q52. How do you decide what to measure and when?

**Answer:**
I think about metrics in three tiers.

**Before launch: what should we track?**
During design, I define what success looks like with the PM and engineering leads. For the AI Assistant, that meant: adoption (user count, session count), satisfaction (like/dislike rate), resolution (escalation rate), and specific interaction patterns we wanted to validate (thread usage, preset menu engagement).

**During beta: what's actually happening?**
The instrumentation was set up before launch. We tracked everything listed above in real time. The key discipline is separating vanity metrics (total user count) from actionable metrics (like rate per response type, escalation patterns by query category).

**After launch: what do we learn?**
The 831 escalated chats were more valuable than the 87.35% like rate. The like rate told us the system was generally working. The escalations told us exactly where it wasn't and gave us a roadmap for improvement. I always look for the metric that tells me what to fix next, not just the one that looks good in a presentation.

---

## SECTION 14: DEEP-DIVE USER RESEARCH PER PROJECT

---

### Q53. Walk me through exactly how you conducted user research for the AI Assistant.

**Answer:**

**Phase 1: Quantitative foundation (support call log analysis)**
I worked with the CS operations team to pull 3,500 support call records from Q3 and Q4 of 2023. These weren't just ticket counts. Each record had the issue category, resolution time, whether the caller was a homeowner or installer, and whether the issue was resolved on the first call.

I categorized every call by type and calculated the percentage of total volume for each. The top 30% of homeowner calls broke down to site status checks (11.9%), gateway connectivity (9.9%), battery issues (4.8%), and system access (3.3%). For installers, it was microinverter PLC issues (8.27%), site checks (6.8%), WiFi (4.9%), gateway replacement (4.85%), and stuck booting (4.67%).

Then I tagged each category as automatable or not. About 60% of total volume fell into the automatable bucket. This gave us the business case and the priority list before we designed anything.

**Phase 2: Qualitative discovery (stakeholder discussions)**
I ran semi-structured conversations with three groups. Not formal usability tests. These were open-ended discussions where I asked people to walk me through their last experience with a problem.

With homeowners, I focused on emotional state. One homeowner said "I get scared when I see an error, especially when I don't know what it means." Another said "If there's a quick fix, I'm okay doing it myself, but I don't want to guess." These told me the AI needed to reassure, not just inform.

With installers, I focused on workflow context. I learned they're standing on rooftops or in basements with a phone in one hand. They said things like "When I'm on-site, I don't have time to read long documents. I need quick answers." This shaped the no-fluff, technical tone.

With CS agents, I focused on operational friction. The biggest insight came from an agent who said "The first 5-10 minutes of every call is just me pulling up information. That could be automatic." Another said 15-18% of their calls were repeat callers just checking on open cases. These insights directly shaped the AI's ability to prefetch system data and show case status.

**Phase 3: Contextual observation**
I sat with CS agents during live calls. I wasn't asking them questions while they worked. I just watched and noted what they did: which screens they opened, what information they searched for, how long they spent gathering context before solving the problem. The 5-10 minute information gathering phase was visible in every single call I observed.

**Phase 4: Desk study (competitive analysis)**
I evaluated existing self-service channels: Enphase's own knowledge base, community forums, product manuals, and competitor chatbot implementations. Each had a specific failure mode. Knowledge base articles were too generic. Forums had inconsistent and sometimes wrong advice. Product manuals were too technical for homeowners. Existing chatbots used rigid decision trees that couldn't handle ambiguous queries.

**Phase 5: Alpha and beta testing**
Alpha was qualitative. A controlled group used the V2 assistant and gave direct feedback. This caught two friction points: the preset menu disappeared after the first message, and feedback buttons were hidden behind a three-dot overflow menu.

Beta was quantitative. 229K users, instrumented for everything. Session counts, message volume, like/dislike on every response, thread switching rates, new chat usage, and escalation tracking. We didn't ask beta users questions. We let the data answer them.

---

### Q54. How did you conduct research for the Solaris 2.0 Design System?

**Answer:**

**The audit as research method:**
For a design system, the research isn't interviews. It's a forensic audit of what exists and how people are using it.

I went through every screen in Solargraf and documented inconsistencies. I found 12+ shades of grey with no naming convention. Spacing values drifted between 12px, 14px, 15px with no pattern. Border radii were 8px on buttons, 10px on cards, 12px on modals. Typography had no shared scale.

Then I looked at how designers were actually using the existing components. The critical finding: designers were detaching components on nearly every use. The Input Card Form, the most used pattern in Solargraf, was detached every single time because it couldn't accommodate different content.

**Talking to designers (my own team):**
I asked the other designer on the team direct questions: "Which components do you detach most often? Why?" and "When you're building a new screen, where do you spend the most time on manual adjustments?" The answers consistently pointed to the same problems: fixed widths, no auto-layout, no way to swap content without breaking the master component.

**Talking to engineers:**
I asked engineers: "When you get a design handoff, what takes the longest to implement?" and "Which values do you end up hard-coding because there's no consistent reference?" This surfaced the token architecture gap. Engineers were referencing hex values directly because there were no semantic names. Every brand color update required finding and replacing values across the codebase.

---

### Q55. How did you conduct research for the Icon Set redesign?

**Answer:**

**Visual audit:**
I documented every icon in the existing Solargraf product. Not just what they looked like, but how they were used. The same icon was reused for "Project" and "View Company," which meant users couldn't build reliable mental models. Stroke weights mixed 1px, 1.5px, and 2px within the same view. Some icons had corner radii, others were sharp. There was no optical size compensation, so icons at the same canvas size appeared different visual sizes.

**Comparative analysis:**
I studied icon systems from products that handle information density well: Figma's Lucide icons, Apple's SF Symbols, Material Design icons. I wasn't copying their style. I was understanding their rules. Every good icon system has a grid, a stroke weight standard, and rules for optical alignment.

**Size testing:**
After defining the 10-rule checklist (24x24 grid, 18px safe zone, 1px stroke, etc.), I rendered every icon at its smallest usage context (16px in sidebar navigation) and largest (48px in onboarding screens). Any icon that lost clarity at 16px or looked visually thin at 48px went back for refinement. This was a manual process. I printed test sheets and reviewed them at actual size.

---

### Q56. How did you conduct research for the AR Troubleshooting Guide?

**Answer:**

**Double diamond approach (thesis project):**
This was my M.Des thesis at IIT Roorkee, so it followed a more formal research structure.

**Discover phase:**
I interviewed three stakeholder groups: homeowners, CS agents, and installers. With homeowners, the focus was on their emotional experience during equipment failures. I learned they felt anxious and helpless, especially during weather events like hurricanes. One persona, Alicia, was a homeowner in Puerto Rico dealing with battery issues during hurricane season. Her story became the narrative anchor for the project.

With CS agents, the key finding was the 30% number: agents estimated that 30% of inbound issues could be self-resolved if homeowners had proper visual guidance. The issues were physical tasks like power cycling batteries, checking LED indicators, and verifying cable connections.

**Define phase:**
I mapped the homeowner's emotional journey from "system functioning normally" through "problem identification," "analysis," "resolution," and "post-resolution." The anxiety peaks at the analysis stage, when they know something is wrong but don't know what to do. That's the intervention point.

I also evaluated existing first-contact resolution channels: blogs (too generic), online communities (inconsistent, delayed), product manuals (too technical to follow while standing in front of hardware). All of them fail at the critical moment when a homeowner needs to do something physical with their equipment.

**Develop phase:**
The insight that AR was the right medium came from the physical nature of the tasks. When someone needs to press a specific button on a battery, reading instructions on a screen and translating them to the physical device introduces error. AR overlays the instruction directly onto the device. No translation needed.

---

## SECTION 15: HOW I ARRIVED AT SOLUTIONS

---

### Q57. How did you go from research findings to the AI Assistant solution? Walk me through the reasoning.

**Answer:**

The solution didn't arrive as one idea. It was assembled from several research insights converging.

**Insight 1: 60% of calls are automatable.**
The call log analysis showed that most support queries were repetitive, factual questions with known answers. This made AI a viable medium because the AI doesn't need to reason creatively. It needs to look up the right information and present it clearly.

**Insight 2: Three personas need fundamentally different experiences.**
The stakeholder discussions made it clear that a homeowner asking "why is my bill high?" and an installer debugging a gateway fault are different problems. Same information system, different presentation. This led to the one AI layer, three persona-adaptive interfaces architecture.

**Insight 3: Context is available at launch.**
When a user opens the assistant from the Homeowner App, the system already knows they're a homeowner and has access to their site data. From the ITK installer app, it knows the installer and the site they're working on. This meant the AI could prefetch context and skip the 5-10 minute information gathering that CS agents described. Only the website required the "who are you?" step because persona isn't known upfront.

**Insight 4: Existing solutions fail at the moment of need.**
The desk study showed that knowledge bases, forums, and manuals all fail because they require the user to search, read, and interpret. The AI could invert this: the user describes the problem, the AI finds and presents the answer.

**Insight 5: The Salesforce V1 taught us what not to do.**
V1's branching logic couldn't handle ambiguity. If a user's question didn't match a predefined path, it dead-ended. This confirmed we needed real LLM capabilities, not a decision tree with a chat skin.

**How these connected:**
60% automatable + persona context at launch + real LLM capabilities = an embedded AI assistant that adapts to who's asking and already knows their system context. The four ingress points (Homeowner App, ITK, Enlighten Manager, Website) were determined by where each persona already spends their time.

---

### Q58. How did you arrive at the design system solution for Solaris 2.0?

**Answer:**

**The audit told me what was broken. The conversations told me why.**

The audit gave me the symptom list: 12+ greys, arbitrary spacing, inconsistent radii, constant component detaching. But the conversations with designers and engineers told me the root cause: there was no abstraction layer between raw values and their meaning.

**Why two-tier tokens instead of just naming colors:**
If I just named the colors (grey-500, blue-400), engineers and designers would still disagree about when to use which one. Semantic tokens solve that. "text-secondary" tells you when to use it. "grey-500" only tells you what it looks like.

The two-tier architecture also future-proofed theme switching. A dark mode only needs new semantic mappings, not new components. This wasn't a current requirement, but the Color Theme Changer plugin I built separately proved the pattern was viable.

**Why slot-based architecture for the Input Card Form:**
The audit showed designers detached the Input Card Form on every use. I asked why: the content inside the card varied across contexts (text inputs, checkboxes, date pickers, dropdowns), and the old component couldn't accommodate that variation.

The slot-based solution came from thinking about the problem as content composition rather than variant proliferation. Instead of building 15 card variants, I built one Card shell with named content slots. Designers swap slot content without detaching. This addressed the root cause (rigidity) rather than the symptom (detaching).

---

### Q59. How did you arrive at the icon design rules? Why those specific constraints?

**Answer:**

Each rule was a direct response to a problem found in the audit.

- **24x24 grid, 18px safe zone:** Industry standard. But specifically chosen because Solargraf uses icons at sizes as small as 16px in sidebar navigation. The 18px safe zone within a 24px grid leaves breathing room that prevents icons from bleeding to the edge at small render sizes.
- **1px stroke weight:** Solargraf's UI is data-dense. Tables, charts, form fields everywhere. Heavier strokes (1.5px, 2px from the old set) created visual noise that competed with the content. 1px keeps icons present but quiet.
- **No corner radius unless shape demands it:** The old set randomly mixed sharp and rounded corners. This rule eliminates the inconsistency at its source.
- **Even number element sizes:** Prevents sub-pixel rendering issues. A 13px element renders differently on 1x and 2x screens. 12px or 14px renders cleanly everywhere.
- **1px minimum gap between elements:** At 16px render size, elements closer than 1px visually merge. This rule maintains separation at every size.
- **Center-aligned strokes:** Ensures consistent alignment across the set.
- **Rounded joins and caps:** Creates a softer visual feel that matches Solargraf's brand positioning as an approachable B2B tool, not a heavy industrial application.

I didn't invent these constraints in isolation. I studied how Lucide, SF Symbols, and Material Design handle similar problems, then adapted the rules to Solargraf's specific context.

---

## SECTION 16: BEHAVIORAL QUESTIONS (STAR FORMAT)

---

### Q60. Tell me about a time you had to convince stakeholders to change direction. (STAR)

**Answer:**

**Situation:** During the AI Assistant beta, the threads bar sat at the top of the chat interface. It showed conversation threads and a "New chat" button. The engineering team had invested significant effort building the threading system, and the PM considered it a key differentiator.

**Task:** I needed to determine whether the threads bar was adding value or taking up space, and if the data supported removal, I needed to convince the team to remove a feature they'd invested in.

**Action:** I pulled the interaction data. Over the beta period with 229K users, fewer than 8% of sessions used the "New chat" button. Thread switching accounted for less than 3% of all interactions. Users were in a hurry to resolve issues and move on. They weren't organizing their chat history.

I presented this data in a team review alongside a side-by-side comparison of the interface with and without the threads bar. The version without it gave significantly more vertical space to the conversation itself, which is what users actually cared about.

**Result:** The team agreed to remove the threads bar and relocate the "New chat" action into the fixed menu bar at the bottom. No pushback once the data was visible. The key was that I didn't frame it as "this feature is bad." I framed it as "users are telling us through their behaviour that screen space for the conversation matters more than thread management."

---

### Q61. Tell me about a time you had to make a decision without enough data. (STAR)

**Answer:**

**Situation:** When designing the AI-to-human agent handoff for the assistant, we didn't have any data on how users would perceive the transition. Would they realize they're now talking to a person? Would they change their communication style? We couldn't A/B test this because it was a first launch.

**Task:** Design a handoff experience that makes the transition unmistakable, without being disruptive.

**Action:** I drew on a cognitive psychology principle I was studying in my IGNOU coursework: environmental context change. When your physical environment shifts, your brain registers a mode change automatically. I applied this by designing a double signal: the assistant icon swaps to a human agent icon, and the chat background shifts from yellow (AI identity color) to the platform's native color. Two simultaneous changes create an environmental context shift.

I prototyped both a subtle version (just a text message saying "You're now connected to an agent") and the double-signal version. In internal reviews, every team member who saw the double-signal version immediately said "oh, I'm talking to a real person now" without reading any text. The subtle version was missed by several reviewers.

**Result:** We shipped the double-signal handoff. During alpha testing, no users reported confusion about whether they were talking to AI or a human after the transition. The psychology principle held in practice.

---

### Q62. Tell me about a time you received critical feedback and changed your approach. (STAR)

**Answer:**

**Situation:** During alpha testing of the AI Assistant V2, I had designed the feedback actions (thumbs up, thumbs down, read aloud, copy) behind a three-dot overflow menu on each AI response. This was a conscious choice for visual cleanliness. I didn't want buttons cluttering every response bubble.

**Task:** Respond to the feedback that this design choice was actively hurting the product.

**Action:** The alpha testers barely used the feedback mechanism. When the PM pointed out that we needed feedback data to train and improve the models, and that burying the controls was working against our most critical product need, I had to accept that my preference for visual cleanliness was in direct conflict with the product's core requirement.

I redesigned the feedback actions to appear directly under every response. It added visual elements to the conversation, but it made the action obvious and frictionless. I also had to reconsider my own bias: I was optimizing for what I thought looked good rather than what the product needed. The product was new, feedback data was existential, and hiding the feedback mechanism was a design decision that looked right but functioned wrong.

**Result:** After surfacing the buttons, feedback engagement increased substantially. We collected 4,358 feedback responses (3,806 likes, 552 dislikes) during beta, which gave us the 87.35% like rate and, more importantly, the failure pattern data from dislikes. That data directly improved the AI models. If I'd kept the overflow menu, we wouldn't have had enough feedback to identify the 831 edge cases where AI confidence was high but accuracy was low.

---

### Q63. Tell me about a time you had to work with ambiguous requirements. (STAR)

**Answer:**

**Situation:** When the AI Assistant project started, the brief was broad: "Build an AI assistant for Enphase customers." There was no specification of which customers, which platforms, what it should sound like, what it shouldn't do, or how it would connect to existing systems.

**Task:** Transform a vague directive into a structured, scoped, buildable product.

**Action:** I started with what I could measure. I pulled the 3,500 support call records to understand what customers were actually asking about. This gave me scope: the top 30% of call volume was the priority. The persona split (homeowner vs installer) gave me the audience. The platform audit (4 existing products) gave me the ingress points.

Then I created constraints where none existed. I adopted Microsoft's 18 AI Design Guidelines and selected 7 that applied to our context. This gave the team a shared framework for every design decision. Instead of debating "should the AI apologize when it's wrong?" we could point to guideline 01 (graceful escalation) and say "yes, and here's how."

I also mapped the four complexity patterns (API fetch, task automation, restricted access, guided troubleshooting) to give engineering clear categories for backend architecture. Each pattern had defined UI flows, confirmation requirements, and fallback behaviors.

**Result:** What started as "build an AI assistant" became a structured system: 3 personas, 4 platforms, 7 design principles, 4 complexity patterns, clear priority order based on call volume data. The structure made every subsequent decision faster because we had a framework to evaluate against.

---

### Q64. Tell me about a time you had to say no to a feature request. (STAR)

**Answer:**

**Situation:** During the AI Assistant design, there was a request from the PM team to add a knowledge base browser within the assistant. The idea was that users could browse help articles directly in the chat interface, like a mini documentation viewer.

**Task:** Evaluate whether this feature aligned with the product's core purpose and push back if it didn't.

**Action:** I reviewed how users were actually interacting with the assistant. They were asking questions in natural language and expecting answers. Nobody was browsing. The desk study had already shown that the existing knowledge base was one of the failing channels because it required users to search, read, and interpret.

I argued that embedding a knowledge base browser inside the assistant would recreate the exact problem we were solving. The AI's job is to understand the question and deliver the answer, not to redirect users to documents they'd have to read themselves. If the AI's answer references a knowledge base article, it should extract the relevant information and present it directly, not link out to a separate reading experience.

**Result:** The knowledge base browser was not built. Instead, the 70+ specialized agents are grounded in the knowledge base content, but they synthesize and present it as direct answers. The user never has to leave the conversation or read a separate article. The PM agreed once I reframed it: "The AI is the knowledge base, just one that talks back."

---

### Q65. Tell me about a time you had to balance competing priorities from different stakeholders. (STAR)

**Answer:**

**Situation:** On the AI Assistant, three stakeholders had different priorities. The CS operations lead wanted to reduce call volume immediately, which meant prioritizing homeowner queries. The installer team lead wanted the assistant on the ITK app because installers were losing billable time waiting on hold. The AI/ML engineering lead wanted to start with the website because it was the simplest integration with the fewest variables.

**Task:** Create a rollout strategy that satisfied all three without diluting focus.

**Action:** I mapped each request against the data. Homeowner call volume was highest (28% on billing alone), so CS operations had a valid point. Installer calls averaged 35 minutes including hold time, so the installer team's urgency was real. Engineering's preference for the website made technical sense because the website had no persona detection, making it the simplest test environment.

I proposed a phased approach: V1 on the website first (validates the technology with engineering's simplest case), V2 across all four platforms simultaneously (addresses homeowner and installer volume at the same time). For V2, persona detection is automatic on the apps, so the homeowner and installer experiences could ship together.

**Result:** V1 launched on the website. V2 launched across all four platforms. The phased approach let engineering validate the LLM integration on the simplest surface first, then scale to persona-adaptive experiences. All three stakeholders got what they needed, just not all at once.

---

## SECTION 17: CHALLENGES AND CONFLICTS I NAVIGATED

---

### Q66. What was the biggest conflict you faced on the AI Assistant project and how did you resolve it?

**Answer:**
The biggest conflict was the V1 to V2 decision. V1 was built on Salesforce with if/else branching logic. It launched, and within weeks it was clear the approach was fundamentally limited. But the engineering team had already invested in the Salesforce integration, and there was organizational pressure to iterate on V1 rather than rebuild.

The conflict was between sunk cost (we've already built this) and user reality (it doesn't work). Conversations felt like IVR menus. The Salesforce design system constrained every layout decision. Branching logic couldn't handle ambiguous queries, which is most of what real users ask.

I documented every failure mode: dead-end conversations where the user's question didn't match a branch, visual constraints where the Salesforce shell blocked our design direction, and the fundamental gap between branching logic and conversational AI. I presented this alongside the call log data showing that 60% of queries were automatable but required natural language understanding, not keyword matching.

The team agreed to a ground-up rebuild. V2 used Claude and Gemini as base models, a custom UI built for our needs, and persona-adaptive responses. It was the right call. V2 scales across 4 platforms and serves 229K users. V1 would have required constant patching to do a fraction of that.

---

### Q67. What was the hardest challenge on the Design System project?

**Answer:**
Getting buy-in for the two-tier token architecture when the team wanted "just give us the components."

The pressure was to skip the foundation and jump straight to building buttons and inputs. Designers wanted components they could drag and drop. Engineers wanted specs they could implement. Nobody was excited about defining 80+ semantic tokens.

The challenge was that without the tokens, every component would be built on hard-coded values, which is the exact problem that created the mess in the first place. If I built 10 components without tokens, and the brand color changed, every component would need manual updates.

I resolved this by building one component (the button) both ways: with hard-coded values and with semantic tokens. Then I simulated a brand color change. The hard-coded version required updating every variant manually. The token version required changing one raw token, and everything updated automatically. That demonstration made the value tangible. The team agreed to define the token architecture before building the remaining components.

---

### Q68. Tell me about a time research findings contradicted your initial design assumption.

**Answer:**
On the AI Assistant, I assumed conversation threads would be a core feature. My reasoning: users would have multiple ongoing topics (billing question, gateway issue, battery concern) and would want them organized separately. I designed a threads bar at the top of the interface with a "New chat" button.

The beta data contradicted this completely. Fewer than 8% of sessions used the "New chat" button. Thread switching was under 3% of interactions. Users treated the assistant as a quick problem-solver. They asked a question, got an answer, and either asked another question or left. They didn't categorize their conversations. They didn't come back to old threads.

This was humbling because the threads feature made logical sense from a design perspective. It's a pattern that works in tools like Slack and ChatGPT where people have long, ongoing, varied conversations. But our users weren't having varied conversations. They had a specific problem, they wanted it solved fast, and they moved on.

I proposed removing the threads bar and relocating the "New chat" action to the fixed menu bar. The data made it obvious. But the deeper lesson was: don't assume that patterns that work in one context transfer to another. Solar energy support isn't a general-purpose chat application.

---

### Q69. How did you handle the tension between visual design and product requirements on the AI Assistant?

**Answer:**
The most visible tension was the feedback buttons. I wanted them hidden. The product needed them visible.

I had designed the AI response bubbles to feel clean and conversational. Adding thumbs up, thumbs down, read aloud, and copy buttons under every response felt cluttered. My instinct was to tuck them behind an overflow menu that appeared on hover or tap.

The PM pushed back. Their argument: this is a new AI product. We have no training data from real users. Every like and dislike feeds directly into model improvement. Burying the feedback mechanism behind an extra tap means most users will never give feedback, and we'll be flying blind on response quality.

They were right. I was prioritizing visual tidiness over the product's most critical data collection mechanism. I surfaced the buttons under every response, adjusted the visual treatment to make them feel less intrusive (smaller size, muted colors until interacted with), and the result was 4,358 feedback responses during beta. That data was worth far more than the visual cleanliness I was optimizing for.

The broader lesson: in a new product, data collection mechanisms are infrastructure, not polish. They should be designed for maximum engagement, not minimum visual footprint.

---

### Q70. What challenges did you face as the sole designer on the icon redesign?

**Answer:**
Two main challenges.

**No external validation loop:** On a team project, other designers catch things you miss. As the sole designer, I had to build my own validation process. I created the 10-rule checklist before drawing a single icon. Every icon was tested against those rules. I also tested at minimum (16px) and maximum (48px) sizes to catch legibility issues I might miss at the design size (24px). This systematic approach replaced the informal peer review that a team would provide.

**Organizational patience:** Redesigning 40+ icons across 4 product areas takes time. There was pressure to "just fix the worst ones and ship." But partial fixes would have created a different kind of inconsistency: some icons following the new rules, some following the old ones. I made the case that the icon set needed to ship as a complete, cohesive system. Half-measures would leave users with an interface that felt even more inconsistent than before, because now there would be two distinct visual languages within the same product.

I resolved this by delivering in batches organized by product area, so each area got a complete set at once. Navigation icons shipped first (most visible, highest impact), then action icons, then status icons, then specialty icons. Each batch was internally consistent from day one.

---

### Q71. How did you navigate the conflict between speed and thoroughness on the interactive playbook?

**Answer:**
The engineering team needed component documentation immediately. The ideal solution was a full Storybook integration with automated component rendering, prop controls, and synced code. That would have taken weeks to set up and maintain.

The conflict was real: ship something imperfect now, or ship something proper later while the team stays blocked. I chose speed, but with a clear boundary. I built a self-contained HTML playbook using Windsurf and Claude Opus in days. Single HTML file, no build system, no dependencies. Developers open it in a browser and it works.

The tradeoff was explicit in how I communicated it: "This is not a replacement for Storybook. This is what we use while the team evaluates their tooling. It covers live component variants, prop controls, and copy-ready code snippets. It does not auto-sync with the Figma library or integrate with CI/CD."

By naming the limitations upfront, there was no confusion about the playbook's role. It filled a gap. It didn't pretend to be the final solution. The team was unblocked within the week, and the conversation about Storybook continued on its own timeline.

---

### Q72. How did you handle the situation where the AR Troubleshooting Guide was well-received but not deployed?

**Answer:**
This was my M.Des thesis project. It received an Honourable Mention at Enphase's Ennovate'23 innovation contest out of 130+ global entries. The CS team validated the 30% self-resolution estimate. The projected impact numbers (50,400+ calls reduced, 25,200+ CS hours saved) were grounded in real data.

But deploying AR in a production mobile app involves significant engineering investment: device compatibility testing, AR framework integration, 3D model creation for every hardware variant, and ongoing maintenance as new products launch. The ROI was clear on paper, but the implementation cost was high relative to other priorities.

I handled this by reframing the value. The thesis work directly informed the AI Assistant's guided troubleshooting pattern. The step-by-step visual guidance approach from the AR concept was adapted into the AI assistant's troubleshooting flows, just without the AR camera overlay. The insight that homeowners need guided, step-by-step physical instructions carried forward even though the AR medium didn't.

In my portfolio, I present the AR project honestly: thesis work, validated research, projected impact, recognized internally, influenced subsequent product decisions. I don't claim it's deployed. That honesty is more credible than overstating the outcome.

---

*Prepared from: somya-portfolio-v4.html, enphase-ai-assistant.html, solaris-design-system.html, solargraf-icon-set.html, ar-troubleshooting-guide.html, resume.html*
