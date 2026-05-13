# Design & Accessibility Guidelines
## Government Mobile Application for Senior Citizens

**Version 1.0 | 2026**
*Ministry of Digital Affairs & Social Services*

---

## Table of Contents

1. [Purpose & Scope](#1-purpose--scope)
2. [Typography & Readability](#2-typography--readability)
3. [Color & Contrast](#3-color--contrast)
4. [Layout & Navigation](#4-layout--navigation)
5. [Interaction Design & Feedback](#5-interaction-design--feedback)
6. [Accessibility Standards](#6-accessibility-standards)
7. [Content & Language Guidelines](#7-content--language-guidelines)
8. [Security, Privacy & Trust](#8-security-privacy--trust)
9. [Testing & Compliance Requirements](#9-testing--compliance-requirements)
10. [Quick Compliance Checklist](#10-quick-compliance-checklist)

---

## 1. Purpose & Scope

*This document defines binding design, accessibility, and usability standards for all government mobile applications targeting senior citizens (65+).*

These guidelines are mandatory for all government agencies and contracted vendors developing mobile applications intended for senior citizen users. Compliance is required for applications to receive official certification and deployment approval.

**Objectives:**

- Ensure that senior citizens can independently use government digital services
- Reduce barriers caused by physical, cognitive, or sensory limitations
- Align with WCAG 2.2 Level AA and national digital accessibility standards
- Build trust and confidence in government digital platforms

---

## 2. Typography & Readability

### 2.1 Font Sizes

*All text must be legible without the user needing to zoom. Use large default sizes and support dynamic text scaling.*

| Text Element | Minimum Size |
|---|---|
| Body / Paragraph text | 18sp (scalable to 22sp) |
| Labels & captions | 16sp minimum |
| Buttons & CTA text | 18sp — bold |
| Section headings (H2) | 22sp — bold |
| Page titles (H1) | 28sp — bold |
| Error / alert messages | 18sp — bold |

### 2.2 Font Requirements

- Use system-default sans-serif fonts (San Francisco on iOS, Roboto on Android)
- Do not use decorative or condensed typefaces
- Support OS-level dynamic text scaling (minimum support: 200% scale)
- Line height must be at least 1.5x the font size for body text
- Avoid all-caps text for body content — use sentence case

---

## 3. Color & Contrast

### 3.1 Contrast Ratios

*Insufficient contrast is the most common barrier for users with age-related vision decline. These minimums are non-negotiable.*

- Normal text (< 18pt): minimum contrast ratio of **4.5:1** against background
- Large text (≥ 18pt bold / ≥ 24pt): minimum contrast ratio of **3:1**
- UI components and graphical elements: minimum **3:1** against adjacent colors
- Focus indicators: minimum **3:1** contrast against surrounding colors

### 3.2 Color Usage Rules

- Never use color alone to convey meaning — always pair with text or icon
- Provide a high-contrast mode toggle in app settings
- Avoid blue/green and red/green color combinations (common color blindness)
- Background colors must use light neutral tones; avoid dark backgrounds by default
- Interactive elements must have a distinct hover/pressed state visible without color

### 3.3 Recommended Color Palette

| Role | Hex | Usage |
|---|---|---|
| Primary | `#1A3E6B` | Main actions, headings |
| Secondary | `#2E75B6` | Interactive elements |
| Success | `#1E7E34` | Confirmations |
| Error | `#B91C1C` | Errors and warnings |
| Background | `#F8F9FA` | Page background |
| Surface | `#FFFFFF` | Cards and containers |

---

## 4. Layout & Navigation

### 4.1 Touch Targets

Small touch targets are a primary cause of frustration and errors for seniors. All interactive elements must meet the following minimum requirements:

- Minimum touch target size: **48 x 48dp** (recommended 56 x 56dp)
- Minimum spacing between adjacent touch targets: **8dp**
- Primary action buttons must be at least 56dp tall and full-width or near-full-width
- Avoid placing critical actions at screen edges or corners

### 4.2 Navigation Principles

- Use a bottom navigation bar with maximum 5 items and icon + label
- Always show a persistent back/home button in the top navigation bar
- Limit navigation depth to **3 levels** — avoid deep hierarchies
- Breadcrumbs or progress indicators must be shown in multi-step flows
- Never use gesture-only navigation as the sole interaction method
- Tab order must follow a logical reading sequence (top-left to bottom-right)

### 4.3 Screen Layout

- Use single-column layouts on mobile — avoid multi-column on screens < 768dp
- Content must not overlap or require horizontal scrolling
- Whitespace: maintain at least **16dp** padding on all sides of content areas
- Avoid scrolling within scrolling — nested scroll areas are prohibited
- Content density must remain low: maximum 5 interactive elements per screen

---

## 5. Interaction Design & Feedback

### 5.1 Forms & Input

- All form fields must have visible labels — never placeholder-only fields
- Input fields must be minimum **48dp tall**
- Auto-fill support must be enabled for all standard fields (name, address, ID)
- Provide clear, inline validation messages immediately after an error
- Never auto-advance to the next field after input is complete
- Provide a numeric keyboard for number-only fields
- Date pickers must offer text input as an alternative to calendar pickers

### 5.2 Confirmations & Feedback

- All critical actions (submit, delete, pay) must require explicit user confirmation
- Success, error, and loading states must always be communicated visually
- Loading indicators must appear within **300ms** of user action
- Toast notifications must remain on screen for minimum **5 seconds**
- Error messages must explain what went wrong and how to fix it — no error codes only
- Provide an undo option for reversible destructive actions

---

## 6. Accessibility Standards

### 6.1 Screen Reader Support

*Full VoiceOver (iOS) and TalkBack (Android) compatibility is mandatory.*

- All images must have descriptive alt text (or marked decorative)
- All interactive elements must have an accessible name and role
- Announce dynamic content changes using live regions (aria-live equivalent)
- Reading order must match visual layout
- No information may be conveyed by visual position alone

### 6.2 Motor Accessibility

- Support switch access and external keyboard navigation on both platforms
- Avoid time-limited interactions — if used, provide a 10x time extension option
- Shake-to-undo and other motion-based interactions must have button alternatives
- Support pointer input (stylus, mouse) in addition to touch

### 6.3 Cognitive Accessibility

- Use plain language — target reading level of **Grade 6** (Flesch-Kincaid)
- Break long tasks into clearly labeled steps (3–5 steps maximum per flow)
- Provide contextual help icons next to complex or government-specific terms
- Offer a simplified mode that reduces options and hides advanced features
- Never auto-expire sessions without a clear, dismissible warning at least 2 minutes prior

---

## 7. Content & Language Guidelines

- Write in the first language of the target region; provide multilingual support for minority languages where required by law
- Use active voice and short sentences (max 20 words per sentence)
- Avoid jargon, acronyms, and legal/technical language in UI copy
- Define all government-specific terms inline or in a glossary accessible from the app
- Use positive, supportive language — avoid negative framing in error messages
- Icons must always be accompanied by text labels — icon-only navigation is prohibited
- Illustrations, if used, must depict diverse senior citizens in positive contexts

---

## 8. Security, Privacy & Trust

### 8.1 Authentication

- Support biometric authentication (Face ID / fingerprint) as primary login method
- PIN fallback must be available — minimum **6-digit PIN**
- Session timeout must be configurable by the user (default: 15 minutes of inactivity)
- Never auto-fill passwords into fields on behalf of the user without prompt
- Provide a visible session indicator showing how long until auto-logout

### 8.2 Privacy Transparency

- Display a plain-language privacy notice before collecting any personal data
- Explain exactly what data is collected and why, in one screen
- Provide in-app access to all data the user has submitted or that is held about them
- Allow users to download or request deletion of their data within the app
- Never share data with third parties without explicit opt-in consent

---

## 9. Testing & Compliance Requirements

### 9.1 Mandatory Testing

| Testing Type | Requirement |
|---|---|
| Automated accessibility audit | Pass 0 critical errors (axe or Deque) |
| Manual screen reader testing | 100% of core user flows — both platforms |
| Usability testing with seniors | Minimum 8 participants aged 65+ |
| Color contrast audit | All screens pass 4.5:1 / 3:1 ratios |
| Touch target audit | All targets ≥ 48dp |
| Performance testing | App loads in < 3s on 4G, < 6s on 3G |
| Security penetration test | Required before each major release |

### 9.2 Certification Process

- Submit accessibility audit report to the Ministry of Digital Affairs
- Provide usability testing summary with senior participant feedback
- Obtain sign-off from the National Accessibility Officer before public launch
- Annual re-certification required; re-test after any major update

---

## 10. Quick Compliance Checklist

*Use this checklist at each design review and before submission for certification.*

- [ ] All body text is 18sp or larger
- [ ] Contrast ratios meet 4.5:1 for normal text
- [ ] Touch targets are minimum 48 x 48dp
- [ ] Navigation depth does not exceed 3 levels
- [ ] All form fields have visible, persistent labels
- [ ] Screen reader labels set for all interactive elements
- [ ] Plain language used throughout (max Grade 6 reading level)
- [ ] Session timeout warning provided with 2-minute notice
- [ ] Privacy notice displayed before data collection
- [ ] Usability tested with minimum 8 seniors aged 65+
- [ ] Automated accessibility audit passed with zero critical errors
- [ ] App loads in under 3 seconds on 4G

---

> **Contact & Support**
> Ministry of Digital Affairs — Accessibility & Inclusion Division
> accessibility@gov.ma | +212 537 00 00 00
> *For waiver requests, technical questions, or certification submissions.*

---

*Confidential — Ministry of Digital Affairs | Version 1.0 | 2026*
