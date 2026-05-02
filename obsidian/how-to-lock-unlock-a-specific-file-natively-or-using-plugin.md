---
title: "How to lock/unlock a specific file natively or using plugin?"
layout: post
date: 2026-05-02T23:21+09:00
category: obsidian
tags: [obsidian, obsidian-community-plugin, self-managenent]
in: TIL
---

# How to lock/unlock a specific file natively or using plugin?

Short version: **not really, at least not as a true per-file lock built into core Obsidian**. Obsidian itself mainly gives you **Reading view** vs **Editing view**, and you can switch with `Ctrl+E` (`Cmd+E` on macOS). That is useful for avoiding accidental edits, but it is **not the same thing as a real lock/unlock mechanism for an individual note**. The long-running forum thread about locking individual notes is framed as a **feature request**, which strongly suggests this is not a solid native feature in core Obsidian. [Source](https://obsidian.md/help/edit-and-read) [Source](https://forum.obsidian.md/t/option-to-lock-editing-of-individual-notes/22162)

So if your goal is **“protect this specific note from accidental edits”**, the practical answer is: **use a plugin**. That’s the engineer’s answer, not the marketing one.

## Best option for per-file lock/unlock: [Note Locker](https://github.com/Felvesthe/note-locker)

If you want the most direct “lock this file / unlock this file” workflow, **Note Locker** is the cleanest fit. It lets you **lock or unlock a note from the context menu**, either in the file explorer or inside the editor. It also remembers locked notes across sessions and keeps the lock even if the file is renamed. In other words: simple idea, properly implemented. [Source](https://github.com/Felvesthe/note-locker)

It is also reasonably validated by public plugin stats: the Obsidian Stats page describes it as a plugin to protect notes from unintended edits by locking them in preview mode, and shows **2,856 downloads**, **14 stars**, and a **51/100 score** in the available snapshot I checked. [Source](https://www.obsidianstats.com/plugins/note-locker)

A practical note, though: **this is accidental-edit protection, not hardcore security**. The plugin’s own FAQ says you can still manually override and edit if needed. So this is a seatbelt, not a bank vault. [Source](https://github.com/Felvesthe/note-locker)

## Best option for folder-level protection: [Force Read Mode](https://github.com/al3xw/force-read-mode)

If your use case is less “one precious file” and more “everything in this folder should open read-only,” then **Force Read Mode** is arguably better. It forces Markdown files in specified paths to always open in **read/preview mode**. That makes it ideal for folders like templates, archived docs, reference notes, or anything you want to treat as mostly immutable. [Source](https://github.com/al3xw/force-read-mode)

It supports path patterns and can be toggled via the Command Palette, which is nice if you want policy-level control rather than hand-locking notes one by one. On the public stats side, it shows **3,738 downloads** and **16 stars** in the available snapshot, so it also looks like a credible option. [Source](https://github.com/al3xw/force-read-mode) [Source](https://www.obsidianstats.com/plugins/force-read-mode)

## Interesting but less mature: [Locked Notes](https://github.com/preslavrachev/obsidian-locked-notes)

There is also **Locked Notes**, which has a more intentional-editing workflow: notes open in preview mode, you **double-click to edit**, and press **`Esc` to lock again**. That is a pretty elegant UX, especially if you like modal behavior. [Source](https://github.com/preslavrachev/obsidian-locked-notes)

That said, it currently looks more experimental than mainstream. Its README says it is **not yet published in the Obsidian community plugins directory**, requires **manual installation**, and its **lock state does not persist between sessions**. So it’s clever, but not my first recommendation if you want stable day-to-day use. [Source](https://github.com/preslavrachev/obsidian-locked-notes)

## My blunt recommendation

If I were choosing like a Lead Engineer who hates accidental breakage:

**Use `Note Locker`** if you want **true note-by-note lock/unlock behavior**. [Source](https://github.com/Felvesthe/note-locker)

**Use `Force Read Mode`** if you want **folder-based protection** for templates, archives, or reference material. [Source](https://github.com/al3xw/force-read-mode)

**Use native Reading view** only if you want a lightweight built-in workaround and can live without a real per-note lock. [Source](https://obsidian.md/help/edit-and-read)
