# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

GoFlow Technology email signature generator — a single-file static web application (`Index.html`, ~1086 lines) built with vanilla HTML5, CSS3, and JavaScript. No build system, no package manager, no external dependencies.

The tool lets GoFlow employees create professional email signatures with three templates (Classic, Modern, Compact), customizable colors, logo upload, and live preview with clipboard copy.

## Running the Project

Open `Index.html` directly in a browser. No server or build step required.

## Architecture

Everything lives in one self-contained `Index.html` file with three inline sections:

- **`<style>` block**: Dark-themed UI using CSS variables (`--bg`, `--surface`, `--accent`, etc.), responsive grid layout (two-column desktop, single-column under 900px), DM Sans + Outfit fonts for UI
- **HTML body**: Two-panel layout — left editor panel (form inputs) and right sticky preview panel with dark/light toggle
- **`<script>` block**: All application logic in vanilla JS

### Key JavaScript Functions

| Function | Role |
|---|---|
| `generateSignature(d, forCopy)` | Core rendering — builds email-safe HTML tables per template. `forCopy` flag adjusts colors for clipboard vs preview |
| `getValues()` | Collects form inputs + hardcoded company data (KVK, BTW, IBAN, address) |
| `updatePreview()` | Re-renders preview on every input change |
| `copySignature()` / `copyHTML()` | Clipboard API with execCommand fallback |
| `setTemplate(tpl)` / `setPreviewMode(mode)` | State toggles |
| `handleLogo(e)` / `removeLogo()` | Logo upload via FileReader → base64 |

### State

Three module-level variables: `currentTemplate`, `logoDataUrl`, `previewMode`.

### Email Signature Rendering

- Uses HTML tables for email client compatibility
- Font stack: Aptos → Calibri → Helvetica Neue → Arial → sans-serif at 13.5pt
- Three color params: primary, accent, muted (user-configurable via color pickers)
- Dark preview mode inverts text colors; copy mode uses original colors
- Logo scaled to max 160x65px (classic/modern) or 90x40px (compact)

## Language

All UI text and labels are in **Dutch (nl)**.
