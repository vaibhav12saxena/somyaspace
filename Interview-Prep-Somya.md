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

*Prepared from: somya-portfolio-v4.html, enphase-ai-assistant.html, solaris-design-system.html, solargraf-icon-set.html, ar-troubleshooting-guide.html, resume.html*
