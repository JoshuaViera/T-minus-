# Mini PRD

**Product name:** T-Minus
**Your name:** Josh
**Date:** August 16, 2026

---

## Problem statement

People with a trip coming up pack from memory, usually the night before. The date sits in their calendar and the list of what to bring sits in their head, so there's nothing telling them how much time is actually left or what still hasn't gone into the bag. They land somewhere without a charger, without a passport, without the one medication they can't buy over the counter, and they spend the first morning of the trip in a drugstore instead of on the beach.

## Users and needs

**Primary user(s):** Leisure travelers with one specific trip on the calendar, packing for themselves in the week before departure.

- As a traveler, I need to see how much time is left before I leave so I know whether I can pack tonight or need to pack now.
- As a traveler, I need to be shown what to pack instead of trying to remember it, so nothing obvious gets left behind.
- As a traveler, I need my list to still be there tomorrow, because packing happens in five-minute bursts across several days.

## Proposed solution

T-Minus is a web app that shows a live countdown to your departure and a packing checklist you tick off as things go in the bag. You enter your trip name and departure date once. The app then runs a timer down to the minute and shows you a starter list split into Essentials, Clothes, and Electronics, which you can add to, delete from, and check off. Everything saves automatically, so you can pack over several days and always see what's left and how long you have to do it.

## Value proposition

Travelers who pack at the last minute from memory use T-Minus, a countdown paired with a checklist, to see the time they have left and the items they still haven't packed in one place. Unlike a calendar reminder or a note on their phone, it makes the deadline and the remaining items visible together, so nothing gets discovered as missing at the gate.

## Requirements

| Requirement | Priority |
|---|---|
| User can enter a trip name and a departure date and time | MVP |
| User can see a live countdown in days, hours, and minutes that updates on its own | MVP |
| User can see a starter packing list grouped into Essentials, Clothes, and Electronics | MVP |
| User can check off an item as packed and uncheck it | MVP |
| User can add a custom item to any of the three categories | MVP |
| User can delete an item from the list | MVP |
| User can see how many items are still unpacked | MVP |
| User can close the app and come back to find the trip date and checked items still saved | MVP |
| User can see a clear "you're off" state when the countdown reaches zero | MVP |
| User can edit the departure date after setting it | MVP |
| User can clear the list and start a new trip | + |
| User can track more than one trip at a time | + |
| User can create their own categories beyond the three defaults | + |
| User can save a packing list as a reusable template | + |
| User can get a reminder notification at a chosen point before departure | + |
| User can share a list with someone else traveling with them | + |

---

### Scope notes

Persistence is in the MVP on purpose. Without it the app resets every time the tab closes, and packing does not happen in one sitting, so the countdown would be the only part that survives. That's the one requirement I'd argue hardest to keep if the build runs long.

Editing the date is in for the same reason. Flights move.
