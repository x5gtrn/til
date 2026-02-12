---
title: "Superkey: Simple and powerful keyboard enhancement on macOS"
layout: post
date: 2026-02-07T21:15+09:00
category: apps
tags:
    - shorcuts
    - keyboard
    - enhancement
---

# [Superkey](https://superkey.app): Simple and powerful keyboard enhancement on macOS

## Core Functionality

**Superkey** is a macOS keyboard enhancement utility that enables users to navigate and interact with their computer more efficiently without relying on a mouse or trackpad. It combines OCR-based screen interaction with powerful keyboard remapping capabilities.

---

## Primary Features

### 1. **Seek & Click**
The flagship feature that allows you to interact with any text on your screen using only your keyboard.

**How it works:**
- Type what you want to click on, and Superkey will find and highlight all matching text on screen
- Navigate between matches and execute clicks entirely via keyboard
- Uses **Optical Character Recognition (OCR)** to detect text anywhere on screen
- Also supports **Accessibility API parsing** for apps that expose UI elements through macOS accessibility framework

**Technical details:**
- Works system-wide across all applications
- Can be triggered by remapping any key (commonly Caps Lock)
- Supports cycling through multiple matches
- Optional: Show only while the trigger key is held down

**Current limitations:**
- Small text may be difficult to detect
- Text very close to lines can be challenging for OCR
- Requires screen recording permissions for screenshot analysis

---

### 2. **Hyperkey**
Converts a single physical key into a "hyper modifier" that combines all four macOS modifiers simultaneously.

**Configuration:**
- Remap **Caps Lock** or any modifier key to Hyperkey
- Hyperkey = ⌃ (Control) + ⌥ (Option) + ⌘ (Command) + ⇧ (Shift) combined
- Acts as an additional modifier layer for keyboard shortcuts

**Use cases:**
- Create custom shortcuts that won't conflict with existing app shortcuts
- Expand your keyboard shortcut namespace significantly
- Compatible with third-party apps like Keyboard Maestro, BetterTouchTool, etc.

**Note:** When recording shortcuts in Keyboard Maestro, physically press all four modifiers rather than using the shortcut recorder's interface. The configured Hyperkey will then properly trigger those shortcuts.

---

### 3. **Power User Presets**
A collection of checkbox-configurable keyboard remappings for maximum efficiency.

**Available remappings include:**
- Custom key substitutions
- Modifier key conversions
- **Left Shift + Right Shift = Caps Lock** (useful when Caps Lock is remapped)
- Additional preset options for common power-user workflows

**Philosophy:** Simple checkbox interface for complex remappings without needing scripting knowledge.

---

## System Requirements & Permissions

### **Compatibility:**
- macOS 12 (Monterey) or later
- Supports both Intel and Apple Silicon Macs

### **Required Permissions:**

1. **Accessibility Access**
    - Detects configured keystrokes
    - Executes simulated clicks
    - Monitors keyboard input for remapping

2. **Screen Recording**
    - Only used for Seek feature
    - Takes screenshots to perform OCR analysis
    - Not used for any other purpose

### **Privacy Commitment:**
- No telemetry or tracking
- No data stored to disk
- Network access only for license validation and updates
- All processing happens locally

---

## Known Limitations & Workarounds

### **Password Fields**
- Key remappings don't work in password input fields
- **Reason:** macOS security prevents 3rd-party apps from monitoring keystrokes in secure fields

### **Permission Sync Issues**
If you encounter "Unable to initialize Superkey" despite granting permissions:

1. Close Superkey completely
2. In System Settings → Privacy & Security → Accessibility:
    - Disable Superkey
    - Remove Superkey from the list
3. Also check Input Monitoring section and remove if present
4. **Restart your Mac**
5. Launch Superkey and re-grant permissions when prompted

---

## Recommended Setup (Creator's Configuration)

**Ryan Hanson's personal Seek setup:**

1. **Remap Caps Lock → Seek trigger**
    - Makes Seek instantly accessible on home row
    - Enable "Show only while key is held" for shortcut-like behavior

2. **Semicolon key → Cycle through results**
    - Natural right-hand positioning for result navigation

3. **Left Shift + Right Shift → Caps Lock**
    - Restores Caps Lock functionality when needed
    - Enabled via Presets tab

---

## Licensing & Pricing

- **Free trial:** 20 days
- **Purchase:** Single license (price listed on website)
- **Multi-device:** One license active on up to 3 devices simultaneously
- **Purchase handled by:** Paddle.com (Merchant of Record)

---

## Technical Architecture

- Native macOS application
- Local OCR processing (no cloud dependency)
- Lightweight menu bar utility
- Minimal system resource usage
- No background internet connectivity except for updates/license validation

---

## Developer

Created by **Ryan Hanson** ([ryanhanson.dev](https://ryanhanson.dev/))

**Support:** superkey@ryanhanson.dev

---

## Summary

Superkey transforms keyboard-first workflows on macOS by combining intelligent screen text detection with powerful key remapping. It's particularly valuable for:

- Users seeking to minimize mouse/trackpad usage
- Power users with extensive keyboard shortcut libraries
- Accessibility-focused workflows
- Efficiency enthusiasts who want faster screen navigation

The app's privacy-first approach and local processing make it suitable for security-conscious users, while its simple checkbox interface keeps advanced features accessible to non-programmers.