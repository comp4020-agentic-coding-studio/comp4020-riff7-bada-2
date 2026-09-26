# You are riffing on someone else's prototype

This repo is a copy of [`comp4020-crit7-bada`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit7-bada) at
`233f9626` --- bada's crit agent's shipped prototype for `07-anu-system`.
The copy is yours; their repo is untouched and off limits.

**The brief is to take this somewhere it hasn't been.** Not to restart it, not
to polish it, and not to finish the agent's to-do list. Read how they directed
the agent, find the thing the prototype implies but doesn't do, and build
that. You have the session's half-hour, so pick something you can get live.

**Nothing here is marked.** No cutoff, no reflection, no `PROCESS.md` entry,
no crit sweep, no repo of your own on the line. That is the point --- the
interesting move is the one you wouldn't risk in your own graded repo.

**What you show at the share-back** is the live site plus
`git diff riff-start`. Push early and keep `main` green.

**The agent's own spec tests are `spec/bookings.test.ts` and `spec/readme.test.ts`.** They encode the crit brief,
not yours, and they gate the deploy --- a red check means no live site to show
at the share-back. If your riff moves past that brief, change them or delete
them; keep `spec/invariants.test.ts` green, since that one is true of any good
site.

Everything below this line was written for that crit submission. The marks,
the cutoff, the private-repo phase, the weekly `start` skill and the
reflection are all done, and none of it governs what you do here. Read it for
how they worked, not for what you owe.

---

# Your harness

This is a tutorial/lab session booking app. The one thing that actually
matters is `bookSession` in `src/lib/db.ts`: a session must never hold more
bookings than its capacity, and the check-then-write has to happen inside a
single `db.transaction` so two concurrent requests can't both pass the check
before either writes. Any change to booking logic needs to preserve that —
don't refactor it into a separate read then a separate write.

The schema (`src/lib/schema.ts`) is ground truth. Change it there, run
`pnpm db:generate`, commit the migration alongside — never hand-edit a
migration or the database file.

`spec/bookings.test.ts` is the contract: filling a session to capacity, a
rejected overflow booking, a rejected duplicate name, and a live SSE
broadcast. Keep it green; extend it rather than weakening an assertion when
a change makes it fail.

Don't add a waitlist, cancellation, or real accounts without deciding that's
this week's actual scope — `README.md` explains why those are deliberately
out for now. Run `pnpm check` before every commit.
