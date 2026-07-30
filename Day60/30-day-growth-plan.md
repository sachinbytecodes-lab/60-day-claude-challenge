# 30-Day Growth Plan — AI Job-Fit Matcher

A realistic, one-milestone-per-day roadmap taking AI Job-Fit Matcher from its v1.0.0 capstone state to a significantly more complete product. Each day assumes ~1-2 hours and builds directly on the previous day's work. Use the accompanying `daily-build-prompt.md` each day, changing only the day number.

## Week 1: Testing Foundation & Quick Wins (Days 1-7)

1. Set up Jest + React Testing Library; write first test for `lib/parseResume.js`
2. Write tests for `lib/aiPrompt.js`'s `validateAndFill` and `extractJson` functions
3. Write an integration test for `/api/analyze`'s validation logic (file type, size, JD length)
4. Add a custom-branded favicon (replace the default) and confirm it renders across browsers
5. Add screenshots to `README.md` (landing, dashboard, results) for portfolio/recruiter readability
6. Add a "How it works" 3-step visual section to the landing page above the fold
7. Week 1 review: run full test suite, confirm nothing broke, commit `v1.1.0-dev` progress

## Week 2: Resume Version History (Days 8-14)

8. Design schema addition: add `resumeVersionLabel` field to `Analysis` model
9. Build UI to let users name/label a resume at upload time (e.g., "Data Analyst v2")
10. Build a simple "compare to previous" view showing fit-score delta between two analyses for the same JD
11. Add a PDF export button on the results page (use a client-side library like `jspdf` or `react-to-print`)
12. Style and test the PDF export across the 3 score ranges (high/medium/low fit)
13. Add a "Download Report" analytics event (simple console log or lightweight tracking) to understand usage
14. Week 2 review: full manual walkthrough of version history + export, deploy to production

## Week 3: Batch Comparison (Days 15-21)

15. Design schema: add `batchId` field to group related analyses (from `future-scope.md`)
16. Build the multi-JD input UI on the Analyze page (start with 2 JDs, one resume)
17. Update `/api/analyze` to accept multiple JDs and loop the existing AI call per JD
18. Build a ranked results view showing all JD matches sorted by fit score
19. Add rate-limit awareness to the batch endpoint (basic in-memory request counting per user)
20. Test batch flow end-to-end with 3+ real JDs against one resume
21. Week 3 review: deploy batch comparison, update README feature list

## Week 4: Polish, Hardening & Public Push (Days 22-30)

22. Add basic per-user rate limiting to `/api/analyze` (the Day 8-deferred item) using a simple in-memory or Vercel KV-based counter
23. Audit and fix any new accessibility gaps introduced by Week 2-3 features
24. Add a lightweight admin view (just for you) showing total analyses run, for your own usage insight
25. Write a "What I learned building this" blog-style post for LinkedIn using the retrospective as source material
26. Record a 60-90 second demo video walking through the app (use the demo script from Day 10's portfolio materials)
27. Post the project publicly on LinkedIn/Twitter with the demo video and live link
28. Respond to any feedback received; log real user-reported issues as GitHub Issues
29. Fix the highest-priority reported issue (if any) or pick one item from `future-scope.md`'s 3-month list
30. Final review day: tag `v1.1.0` release on GitHub, update `challenge-retrospective.md` with a "30 days later" addendum

## How to Use This Plan

Each day, open a fresh AI conversation and paste in `daily-build-prompt.md`, replacing only the day number. The prompt will reference this file and pick up exactly where the previous day left off — no need to re-explain the project each time.
