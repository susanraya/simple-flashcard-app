# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECHSTACK · approved · source: requirements:technology-stack

Product owner approved an exact technology stack for the build: FastAPI backend, AWS cloud, PostgreSQL database, React frontend.

Decision: design against exactly Backend=FastAPI, Cloud=AWS, Database=PostgreSQL, Frontend=React; no substitutions permitted. Delivery scope flagged as 'lightweight', requirements version 1.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004, EPIC-005, EPIC-006

### REQ-EPIC-001 · draft · source: requirements:EPIC-001

Learner Accounts and Private Access: email-and-password accounts via a hosted auth provider, single 'learner' role, sign-up/sign-in/sign-out, and strict per-account data privacy.

Assumptions: accounts required (no local-only/no-login alternative); exactly one role (learner, no admin/teacher); app is entirely free (no billing surfaces); no emails/notifications beyond what the auth provider itself requires.
- US-001 (critical) Sign up: valid email+password creates account via hosted auth provider, signs in, lands on empty deck list (AC-001); duplicate email blocked with message + sign-in link, no second account (AC-002); malformed email/invalid password shows inline field-specific error (AC-003); no payment/plan/billing ever requested (AC-004).
- US-002 (critical) Sign in: correct credentials sign in and show the account's decks (AC-005); incorrect credentials show one generic error that doesn't reveal account existence (AC-006); cross-device sign-in shows the same decks (AC-007); only email+password offered, no social/SSO (AC-008).
- US-003 (high) Sign out: ends session, returns to sign-in (AC-009); after sign-out, back button or direct deck/study URLs redirect to sign-in with no content shown (AC-010).
- US-004 (critical) Data privacy: learner A never sees learner B's decks/cards/history anywhere in the list (AC-011); requesting another learner's resource by ID is refused server-side (AC-012); unauthenticated requests to any learner-data screen redirect to sign-in (AC-013); no sharing, publishing, or public deck library exists anywhere in the app (AC-014).

**Related:** US-001, US-002, US-003, US-004, AC-001, AC-002, AC-003, AC-004, AC-005, AC-006, AC-007, AC-008, AC-009, AC-010, AC-011, AC-012, AC-013, AC-014

- ⚠ AC-001 and AC-003 reference password rules ('meets the stated rules' / 'fails the stated rules') but no actual password policy (length, complexity) is defined anywhere in the provided input.

### REQ-EPIC-002 · draft · source: requirements:EPIC-002

Deck Management: the deck list is the home screen and sole way to find decks; decks can be created, renamed, and deleted with cascading confirmation.

Assumptions: decks found only by scrolling (no search/filter/tag/folder); deleting a deck permanently removes its cards and study history behind a confirmation prompt.
- US-005 (critical) Home screen lists each deck by name + card count with study/open actions (AC-015); empty state with 'create first deck' action when no decks exist (AC-016); list reachable purely by scrolling, no search/tag/folder UI (AC-017).
- US-006 (critical) Create deck: non-empty name saves a zero-card deck that appears in the list (AC-018); empty/whitespace name rejected with required-field message (AC-019); deck persists across sign-ins/devices (AC-020).
- US-007 (high) Rename deck: non-empty new name saved and reflected in list (AC-021); empty/whitespace name rejected (AC-022); cancel preserves original name (AC-023); cards and history are unaffected by rename (AC-024).
- US-008 (high) Delete deck: confirmation prompt names the deck and warns cards+history will be deleted (AC-025); confirming permanently deletes deck, cards, and session history (AC-026); cancel/dismiss leaves everything unchanged (AC-027); deleted deck's sessions disappear from progress history, other decks unaffected (AC-028).

**Related:** US-005, US-006, US-007, US-008, AC-015, AC-016, AC-017, AC-018, AC-019, AC-020, AC-021, AC-022, AC-023, AC-024, AC-025, AC-026, AC-027, AC-028

### REQ-EPIC-003 · draft · source: requirements:EPIC-003

Card Management: plain-text two-sided cards added one at a time, viewable, editable, and deletable within a deck.

Assumptions: plain text only (no images/audio/rich text); no bulk paste, CSV import, or export; cards browsed by scrolling only, no search/tagging.
- US-009 (critical) Add card: non-empty front+back saves card to deck list (AC-029); empty front/back/both rejected with inline required message (AC-030); form clears after successful submit for rapid re-entry (AC-031); only plain-text fields offered, no image/audio/formatting/bulk-import (AC-032).
- US-010 (high) View cards: all cards in a deck listed with front, back, edit, delete actions (AC-033); empty deck shows empty-state + prompt to add first card (AC-034); long lists reachable by scrolling (AC-035).
- US-011 (high) Edit card: edit form pre-filled with current text (AC-036); saving with both fields non-empty updates card (AC-037); saving with either field empty is rejected (AC-038); cancel preserves original text (AC-039).
- US-012 (medium) Delete card: confirm-and-delete permanently removes card from list (AC-040); cancel leaves card unchanged (AC-041); deleted cards are excluded from subsequent study sessions and totals (AC-042).

**Related:** US-009, US-010, US-011, US-012, AC-029, AC-030, AC-031, AC-032, AC-033, AC-034, AC-035, AC-036, AC-037, AC-038, AC-039, AC-040, AC-041, AC-042

### REQ-EPIC-004 · draft · source: requirements:EPIC-004

Study Session: whole-deck sessions in shuffled order, flip-to-reveal, right/wrong marking, with wrong cards repeating until every card is answered correctly once.

Assumptions: whole-deck sessions only (no length limit, no resume); wrong-card repeats are scoped to the current session only, nothing remembered between sessions (no spaced repetition).
- US-013 (critical) Start session: begins with every card in the deck, shows first front (AC-043); no subset-length or resume options offered (AC-044); zero-card deck blocks start with a prompt to add a card (AC-045); in-session progress (cards remaining) is visible (AC-046).
- US-014 (high) Shuffle: order randomized and not simply add-order (AC-047); re-shuffled independently each new session (AC-048); every card appears exactly once in the first pass (AC-049).
- US-015 (critical) Flip: only front shown initially, reveal action available (AC-050); reveal shows back and enables marking (AC-051); marking unavailable before reveal (AC-052); reveal and marking fully keyboard-operable (AC-053, assumption: only sensible keyboard/contrast defaults, no formal accessibility standard specified).
- US-016 (critical) Mark right/wrong: right removes card from queue and advances (AC-054); wrong re-queues card for later in session and advances (AC-055); a repeated card later marked right clears the queue but never counts as first-time-correct (AC-056); session ends when nothing remains unanswered/queued (AC-057).
- US-017 (critical) Repeat wrong cards: first pass completion triggers replay of wrong cards (AC-058); repeated wrong marks re-queue again (AC-059); session cannot end while cards remain queued (AC-060); a new session treats all cards equally regardless of prior-session difficulty (AC-061).

**Related:** US-013, US-014, US-015, US-016, US-017, AC-043, AC-044, AC-045, AC-046, AC-047, AC-048, AC-049, AC-050, AC-051, AC-052, AC-053, AC-054, AC-055, AC-056, AC-057, AC-058, AC-059, AC-060, AC-061

### REQ-EPIC-005 · draft · source: requirements:EPIC-005

Session Results and Deck Progress: end-of-session right-first-time score and a lightweight per-deck session history.

Assumptions: progress tracking deliberately lightweight (score + session list only, no streaks/charts/badges/cross-deck stats/per-card difficulty); deck deletion also deletes its session history (see EPIC-002).
- US-018 (critical) Score: result screen shows right-first-time count out of deck total once every card answered correctly at least once (AC-062); later correct answers for cards missed initially don't count toward the score, e.g. 7/10 example (AC-063); result screen offers 'study again' or 'return to deck list' (AC-064); date and score are saved to the deck's history (AC-065).
- US-019 (high) Progress over time: two-or-more completed sessions show a most-recent-first list with date and score (AC-066); zero sessions shows empty-state message (AC-067); only the per-deck session list is shown, no streaks/charts/badges/cross-deck stats (AC-068); abandoned (incomplete) sessions are not recorded (AC-069).

**Related:** US-018, US-019, AC-062, AC-063, AC-064, AC-065, AC-066, AC-067, AC-068, AC-069

### REQ-EPIC-006 · draft · source: requirements:EPIC-006

Responsive Web Experience and Platform Foundations: one responsive SPA + small server covering phone and desktop, free and English-only, with server-side persistence and basic reliability.

Assumptions: React+TypeScript SPA, small server API, PostgreSQL, managed cloud hosting, single small instance (tens of users, thousands of cards), no HA/scaling work; English-only, no localisation; no accessibility standard beyond sensible defaults; no third-party integrations, import/export, or notifications beyond what auth requires.
- US-020 (high) Responsive layout: phone screens fit without horizontal scroll, all actions reachable/tappable (AC-070); desktop uses wider space sensibly with full action parity (AC-071); rotation mid-session keeps study screen usable without losing progress (AC-072); no offline mode, PWA install, or app-store app offered (AC-073).
- US-021 (critical) Reliable per-account storage: data persists across cleared browser/device changes (AC-074); failed saves show a clear error and do not display false success (AC-075); screens load within a few seconds at personal scale on a single small instance (AC-076).
- US-022 (medium) Free, English-only, no extras: no pricing/plan/upsell/billing anywhere (AC-077); all content in English, no language switcher (AC-078); no reminders, marketing emails, or push notifications (AC-079); no import/export/third-party integrations (AC-080).

**Related:** US-020, US-021, US-022, AC-070, AC-071, AC-072, AC-073, AC-074, AC-075, AC-076, AC-077, AC-078, AC-079, AC-080
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-09-11

**Capabilities in scope:** Learner sign-up, sign-in and sign-out, Private decks tied to the learner's account, Deck list as the home screen, Create a deck with a name, Rename a deck, Delete a deck with a confirmation prompt, Add a card with a plain-text front and back, one at a time, View all cards in a deck, Edit a card, Delete a card, Start a study session on a whole deck, Shuffled card order within a session, Flip a card to reveal the back, Mark each card right or wrong, Wrong cards come round again until answered correctly, End-of-session score: right first time out of total, Responsive phone and desktop layout, Free to use — no plans, subscriptions or billing, Email-and-password sign-in via a hosted auth provider, no social login or SSO, A session always covers the whole deck — no '20 cards' limit or resume, Nothing remembered about card difficulty between sessions, Deleting a deck also deletes its cards and study history, Decks are found by scrolling the list — no search or tags, English-only interface

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | — |
| cloud | AWS | — |
| database | PostgreSQL | — |
| frontend | React | — |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Learner Accounts and Private Access

Email-and-password accounts so a learner's decks persist and follow them between phone and laptop. Sign-up, sign-in and sign-out only; everything a learner creates is private to their account.

Assumptions surfaced: (1) Accounts are required and use email-and-password via a hosted auth provider — no social login or SSO. The alternative considered was a no-login app storing decks only in the browser, which is simpler but loses cross-device access. (2) There is exactly one role, the learner — no admin, teacher or support role. (3) The app is entirely free: no plans, subscriptions, billing or payment surfaces anywhere in the product (assumed, not asked). (4) No emails beyond what the hosted auth provider itself requires — no study reminders or notifications of any kind.

### US-001: Sign up for an account

**Priority:** critical

> As a new learner, I want to create an account with my email address and a password, so that my decks are saved and available whenever I come back.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am on the sign-up screen and not signed in | I enter a valid email address and a password that meets the stated rules and submit | an account is created via the hosted auth provider, I am signed in, and I land on my (empty) deck list |
| AC-002 | I am on the sign-up screen | I submit an email address that already has an account | no second account is created and I see a message telling me the email is already registered, with a link to sign in |
| AC-003 | I am on the sign-up screen | I submit a malformed email address or a password that fails the stated rules | the account is not created and I see an inline message naming the field that is wrong and what is required |
| AC-004 | the product is free to use | I complete sign-up | I am never asked for payment details, plan choice or billing information at any point |

### US-002: Sign in to an existing account

**Priority:** critical

> As a returning learner, I want to sign in with my email and password, so that I can reach the decks I created on another device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-005 | I have an existing account and am signed out | I submit my correct email and password | I am signed in and taken to my deck list showing the decks on my account |
| AC-006 | I have an existing account | I submit an incorrect email or password | I am not signed in and I see a single generic 'email or password is incorrect' message that does not reveal whether the email exists |
| AC-007 | I signed in on my laptop and created a deck | I sign in with the same account on my phone | the same deck appears in my deck list on the phone |
| AC-008 | the sign-in screen is shown | I look at the available sign-in options | only email-and-password is offered, with no social login or SSO buttons |

### US-003: Sign out

**Priority:** high

> As a signed-in learner, I want to sign out, so that nobody else using this device can reach my decks.

| ID | Given | When | Then |
|---|---|---|---|
| AC-009 | I am signed in | I choose Sign out | my session ends and I am returned to the sign-in screen |
| AC-010 | I have just signed out | I use the browser back button or paste a deck or study URL directly | I am not shown any deck or card content and I am sent to the sign-in screen |

### US-004: Keep every learner's data private to their account

**Priority:** critical

> As a learner, I want my decks, cards and study history to be visible only to me, so that my study material stays a private tool and not a shared one.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | learner A and learner B both have accounts with decks | learner A is signed in and views the deck list | only learner A's decks are shown and none of learner B's decks, cards or session history appear anywhere |
| AC-012 | I am signed in as learner A | I request a deck, card or session record belonging to learner B by its identifier | the server refuses the request and no data from that record is returned or displayed |
| AC-013 | I am not signed in | I request any deck, card, study or history screen | I am redirected to sign in and no learner data is returned |
| AC-014 | the product is a private study tool | I look through the whole app | there is no sharing, publishing, public deck library or way to view another person's decks or progress |

## EPIC-002: Deck Management

Create, list, rename and delete decks. The deck list is the home screen and is the only way decks are found.

Assumptions surfaced: (1) Decks are found by scrolling the list — no search, filtering, tagging or folders are included. (2) Deleting a deck also permanently deletes its cards and its study history, behind a confirmation prompt.

### US-005: See my decks on the home screen

**Priority:** critical

> As a signed-in learner, I want my decks listed as the first thing I see, so that I can pick one and start studying straight away.

| ID | Given | When | Then |
|---|---|---|---|
| AC-015 | I am signed in and have one or more decks | I land on the home screen | each of my decks is listed by name with its card count, and each entry offers a way to study it and a way to open it |
| AC-016 | I am signed in and have no decks yet | I land on the home screen | I see an empty-state message explaining I have no decks and a clear action to create my first deck |
| AC-017 | I have more decks than fit on one screen | I view the deck list | I can reach every deck by scrolling, with no search box, tag filter or folder navigation offered (assumption: search and tagging are out of scope for this version) |

### US-006: Create a deck

**Priority:** critical

> As a learner, I want to create a new deck by giving it a name, so that I have somewhere to put cards on a topic.

| ID | Given | When | Then |
|---|---|---|---|
| AC-018 | I am signed in on the deck list | I choose to create a deck, enter a non-empty name and confirm | the deck is saved to my account with zero cards and appears in my deck list |
| AC-019 | I am creating a deck | I submit an empty or whitespace-only name | the deck is not created and I see a message that a name is required |
| AC-020 | I have just created a deck | I sign in again later or on another device | the deck is still listed with the name I gave it |

### US-007: Rename a deck

**Priority:** high

> As a learner, I want to change a deck's name, so that I can correct a typo or re-label a topic as my study changes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-021 | I have an existing deck | I open its rename action, enter a new non-empty name and confirm | the deck is saved under the new name and the deck list shows the new name |
| AC-022 | I am renaming a deck | I submit an empty or whitespace-only name | the name is not changed and I see a message that a name is required |
| AC-023 | I am renaming a deck | I cancel instead of confirming | the deck keeps its original name |
| AC-024 | a deck has cards and past session results | I rename it | its cards and study history are unchanged and remain attached to the deck |

### US-008: Delete a deck with confirmation

**Priority:** high

> As a learner, I want to delete a deck I no longer need, after confirming, so that my deck list stays tidy and I cannot wipe a deck by accident.

| ID | Given | When | Then |
|---|---|---|---|
| AC-025 | I have a deck with cards and past session results | I choose Delete on that deck | a confirmation prompt appears naming the deck and warning that its cards and study history will also be deleted |
| AC-026 | the delete confirmation prompt is showing | I confirm | the deck, all of its cards and all of its session history are permanently deleted and the deck no longer appears in my deck list |
| AC-027 | the delete confirmation prompt is showing | I cancel or dismiss it | nothing is deleted and the deck, its cards and its history remain unchanged |
| AC-028 | I have deleted a deck | I view my progress history | no sessions for the deleted deck are shown, and my other decks and their history are unaffected |

## EPIC-003: Card Management

Add, view, edit and delete plain-text two-sided cards within a deck. Cards are written one at a time through a form.

Assumptions surfaced: (1) Cards are plain text only — no images, audio or rich-text formatting. (2) There is no bulk paste, CSV import or any export in this version. (3) Cards within a deck are browsed by scrolling the list; there is no card search or tagging.

### US-009: Add a card to a deck

**Priority:** critical

> As a learner, I want to add a card by typing a front and a back as plain text, so that I can build up the material I want to study.

| ID | Given | When | Then |
|---|---|---|---|
| AC-029 | I have a deck open | I use the add-card form, enter non-empty plain text for both front and back and submit | the card is saved to that deck and appears in the deck's card list |
| AC-030 | I am adding a card | I submit with an empty front, an empty back, or both empty | the card is not saved and I see an inline message that both front and back are required |
| AC-031 | I have just added a card | the form is submitted successfully | the form is cleared and ready for the next card so I can keep adding one at a time without leaving the screen |
| AC-032 | the add-card form is shown | I inspect what a card can contain | only plain-text front and back fields are offered, with no image, audio, formatting or bulk-import option (assumption: these are out of scope for this version) |

### US-010: View all cards in a deck

**Priority:** high

> As a learner, I want to see every card in a deck with both sides, so that I can check what is in it and spot anything wrong before studying.

| ID | Given | When | Then |
|---|---|---|---|
| AC-033 | a deck of mine contains cards | I open that deck | every card in the deck is listed showing its front and its back, with edit and delete actions available on each |
| AC-034 | a deck of mine contains no cards | I open it | I see an empty-state message and a prompt to add the first card |
| AC-035 | a deck contains more cards than fit on one screen | I view the card list | I can reach every card by scrolling the list |

### US-011: Edit a card

**Priority:** high

> As a learner, I want to change the front or back text of an existing card, so that I can fix mistakes without deleting and re-typing the card.

| ID | Given | When | Then |
|---|---|---|---|
| AC-036 | I am viewing a deck's card list | I choose Edit on a card | a form opens pre-filled with that card's current front and back text |
| AC-037 | the edit form is open with changes made | I save with both fields non-empty | the card's new front and back are stored and shown in the card list |
| AC-038 | the edit form is open | I save with the front or back emptied | the change is rejected and I see a message that both front and back are required |
| AC-039 | the edit form is open with changes made | I cancel | the card keeps its original front and back text |

### US-012: Delete a card

**Priority:** medium

> As a learner, I want to remove a card from a deck, so that I stop being tested on material I no longer need.

| ID | Given | When | Then |
|---|---|---|---|
| AC-040 | I am viewing a deck's card list | I choose Delete on a card and confirm | the card is permanently removed from the deck and no longer appears in the card list |
| AC-041 | I have chosen Delete on a card | I cancel the confirmation | the card remains in the deck unchanged |
| AC-042 | I have deleted a card from a deck | I start a new study session on that deck | the deleted card is not included and the session total reflects the remaining card count |

## EPIC-004: Study Session

Start a session on a whole deck, work through its cards in shuffled order, flip to reveal the back, mark each right or wrong, and have the wrong ones come round again until every card has been answered correctly once.

Assumptions surfaced: (1) A session always covers the whole deck — there is no 'study only 20 cards' length limit and no partial-session resume. (2) Cards marked wrong repeat at the end of the same session only; nothing is remembered about a card's difficulty between sessions, and there is no spaced repetition or 'due today' queue.

### US-013: Start a study session on a deck

**Priority:** critical

> As a learner, I want to start a session covering the whole deck, so that I can test myself on everything I have put in it.

| ID | Given | When | Then |
|---|---|---|---|
| AC-043 | I have a deck containing at least one card | I choose Study on that deck | a session begins containing every card in the deck and the first card's front is shown |
| AC-044 | I am starting a session | the session is set up | I am not offered any option to limit the session to a subset such as 20 cards, and no 'resume previous session' option is presented (assumption: whole-deck sessions only, no resume) |
| AC-045 | a deck of mine contains no cards | I try to study it | the session does not start and I am told the deck needs at least one card, with a prompt to add one |
| AC-046 | I am in a session | I look at the screen | I can see my progress through the session, such as how many cards remain to be answered correctly |

### US-014: See cards in shuffled order

**Priority:** high

> As a learner, I want the cards presented in a random order each time, so that I learn the material rather than the sequence of the list.

| ID | Given | When | Then |
|---|---|---|---|
| AC-047 | a deck with several cards | I start a session | the cards are presented in a randomised order that is not simply the order they were added |
| AC-048 | I have finished a session on a deck | I start another session on the same deck | the cards are shuffled again independently of the previous session's order |
| AC-049 | a session has started with a shuffled order | I work through the session | every card in the deck appears exactly once in the first pass, with none skipped or repeated in that pass |

### US-015: Flip a card to reveal the back

**Priority:** critical

> As a learner, I want to see only the front until I choose to reveal the back, so that I genuinely test my recall before checking the answer.

| ID | Given | When | Then |
|---|---|---|---|
| AC-050 | a card is presented in a session | it first appears | only the front text is shown, the back text is not visible on screen, and a reveal action is available |
| AC-051 | a card's front is showing | I choose to reveal | the back text is shown alongside or in place of the front, and the right and wrong marking actions become available |
| AC-052 | a card's front is showing and has not been revealed | I look for the marking actions | I cannot mark the card right or wrong until I have revealed the back |
| AC-053 | I am on the study screen using a keyboard | I use the keyboard to reveal and to mark right or wrong | each of those actions can be completed without a mouse or touch (assumption: sensible keyboard and contrast defaults only; no formal accessibility standard has been specified) |

### US-016: Mark a card right or wrong

**Priority:** critical

> As a learner, I want to mark each revealed card as right or wrong, so that the session knows what I have learned and what I still need to see.

| ID | Given | When | Then |
|---|---|---|---|
| AC-054 | a card's back has been revealed | I mark it right | the card is recorded as answered correctly, it is removed from the remaining queue, and the next card's front is shown |
| AC-055 | a card's back has been revealed | I mark it wrong | the card is recorded as missed, it is queued to come round again later in this session, and the next card's front is shown |
| AC-056 | I marked a card wrong earlier in this session | that card comes round again and I mark it right | it is cleared from the remaining queue but it still does not count towards my 'right first time' score |
| AC-057 | I have marked the last remaining card | no cards remain unanswered or queued for repeat | the session ends and the result screen is shown |

### US-017: Repeat wrong cards until answered correctly

**Priority:** critical

> As a learner, I want the cards I got wrong to come round again at the end of the session, so that I finish only when I have got everything right at least once.

| ID | Given | When | Then |
|---|---|---|---|
| AC-058 | I have marked some cards wrong during the first pass | the first pass through the deck finishes | the session continues with the cards I marked wrong, presented again |
| AC-059 | a repeated card is presented again | I mark it wrong once more | it is queued again and will reappear later in the same session |
| AC-060 | cards are still queued for repeat | I look at the session | the session does not end until every card in the deck has been answered correctly at least once |
| AC-061 | I marked a card wrong in a previous session | I start a new session on that deck | that card is treated exactly like every other card, with no extra weighting or earlier scheduling (assumption: nothing is remembered about card difficulty between sessions) |

## EPIC-005: Session Results and Deck Progress

Show a score at the end of each session and keep a lightweight per-deck history so the learner can see how a deck is going over time.

Assumptions surfaced: (1) Progress tracking is deliberately lightweight — a per-session score plus a simple per-deck session history. No streaks, charts, badges, cross-deck statistics or per-card difficulty tracking. (2) Session history for a deck is deleted with the deck.

### US-018: See my score at the end of a session

**Priority:** critical

> As a learner, I want to see how many cards I got right first time out of the deck total, so that I know how well I actually knew the material.

| ID | Given | When | Then |
|---|---|---|---|
| AC-062 | I have answered every card in the session correctly at least once | the session ends | a result screen shows the number of cards I marked right on their first appearance out of the total number of cards in the deck |
| AC-063 | a 10-card deck where I marked 7 right on first appearance and 3 wrong before later getting them right | the result screen is shown | the score reads 7 out of 10, with the later correct answers not counted as first-time correct |
| AC-064 | the result screen is shown | I look at my options | I can study the same deck again or return to my deck list |
| AC-065 | a session has just ended | the result is displayed | the session's date and score are saved against that deck on my account |

### US-019: See how a deck is going over time

**Priority:** high

> As a learner, I want to see my past session scores for a deck, so that I can tell whether I am improving on that material.

| ID | Given | When | Then |
|---|---|---|---|
| AC-066 | I have completed two or more sessions on a deck | I view that deck's progress | I see a simple list of past sessions, most recent first, each showing the date and the right-first-time score out of the total |
| AC-067 | I have never completed a session on a deck | I view that deck's progress | I see an empty-state message saying there is no study history yet for this deck |
| AC-068 | I am viewing deck progress | I look at what is presented | only the per-deck session list is shown, with no streaks, charts, badges or cross-deck statistics (assumption: progress tracking is deliberately lightweight in this version) |
| AC-069 | I abandon a session part-way through without answering every card | I return to the deck's progress | no result is recorded for that abandoned session (assumption: sessions are not resumable and only completed sessions are scored) |

## EPIC-006: Responsive Web Experience and Platform Foundations

One responsive browser app that works equally well on a phone and a desktop, backed by a small server storing decks, cards and session results per account.

Assumptions surfaced: (1) Technology is assumed to be a React + TypeScript single-page web app with a small server API and PostgreSQL, on managed cloud hosting in the user's home region, on a single small instance given the low scale (tens of users, thousands of cards) — no high-availability or horizontal-scaling work. (2) The interface is English-only with no localisation. (3) No accessibility standard beyond sensible defaults (keyboard operation of the study screen, readable contrast) has been specified. (4) No third-party integrations, no import or export, and no notifications or emails other than those the hosted auth provider requires.

### US-020: Use the app equally well on phone and desktop

**Priority:** high

> As a learner who studies on both my phone and my laptop, I want the app to lay out sensibly on whatever screen I am using, so that I can study wherever I happen to be without a second app.

| ID | Given | When | Then |
|---|---|---|---|
| AC-070 | I open the app on a phone-sized screen | I view the deck list, a deck's cards and the study screen | the layout fits the width without horizontal scrolling and all actions are reachable and tappable |
| AC-071 | I open the app on a desktop browser | I view the same screens | the layout uses the wider screen sensibly and every action available on the phone is available here |
| AC-072 | I am mid-session on a phone | I rotate the device between portrait and landscape | the study screen remains usable and my session progress is not lost |
| AC-073 | the product is a responsive browser app | I look for an offline mode, installable app or app-store download | none is offered and the app requires a network connection (assumption: offline study, PWA install and native apps are out of scope) |

### US-021: Have my decks, cards and results stored reliably per account

**Priority:** critical

> As a learner, I want everything I create stored on the server against my account, so that nothing is lost when I change device or clear my browser.

| ID | Given | When | Then |
|---|---|---|---|
| AC-074 | I have created decks, cards and completed sessions while signed in | I clear my browser data and sign in again | all of my decks, cards and session history are still present and unchanged |
| AC-075 | I save a deck, card or session result | the server cannot be reached or returns an error | I see a clear message that the change was not saved and the screen does not show the change as if it had succeeded |
| AC-076 | an account holding up to a few thousand cards across decks | I open the deck list, open a deck or start a session | the screen loads within a few seconds on a single small hosted instance (assumption: personal scale, no special performance or high-availability work) |

### US-022: Use a free, English-only app with no extra services attached

**Priority:** medium

> As a learner, I want a single free tool in English with nothing bolted on, so that the app stays simple and I am never interrupted by upsells or noise.

| ID | Given | When | Then |
|---|---|---|---|
| AC-077 | I use every screen in the app | I look for pricing, plans, upgrade prompts or billing settings | none exist anywhere in the product (assumption: the app is entirely free; this was assumed rather than asked) |
| AC-078 | I use the app | I read the interface text | all labels, messages and content are in English and no language switcher is offered (assumption: English-only, no localisation) |
| AC-079 | I have an account | time passes without me using the app | I receive no study reminders, marketing emails or push notifications of any kind |
| AC-080 | I am managing decks and cards | I look for import, export or third-party connections | none are offered (assumption: no bulk/CSV import, no export and no integrations in this version) |
<!-- sdlc:auto:end epics -->
