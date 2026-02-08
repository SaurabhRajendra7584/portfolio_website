# Event Flow & Architecture Diagram

## 1. Complete Event Tracking Flow

```
USER ACTION (Website)
       ↓
   [Browser]
       ↓
DATA LAYER EVENT PUSH
(JavaScript object with event name & parameters)
       ↓
GOOGLE TAG MANAGER
├─→ [Trigger Check] Does event match trigger?
│   ├─ YES → [Tag Fires] → GA4 Measurement Protocol
│   └─ NO → Event ignored
       ↓
GOOGLE ANALYTICS 4
├─→ [Process Event]
├─→ [Validate Parameters]
├─→ [Check Conversions]
├─→ [Update Real-time]
└─→ [Store in Database]
       ↓
REAL-TIME REPORT
├─→ Active Users
├─→ Events (last 30 min)
└─→ Conversions
       ↓
LOOKER STUDIO DASHBOARD
(24 hours later - full data)
```

---

## 2. Data Layer Structure

```
window.dataLayer (Array)
├── [0] {
│   event: 'page_view',
│   page_title: 'Saurabh Rajendra',
│   page_path: '/',
│   timestamp: '2025-02-07T10:30:45.123Z'
│ }
├── [1] {
│   event: 'navigation_click',
│   nav_text: 'About',
│   nav_link: '#about',
│   timestamp: '2025-02-07T10:30:50.456Z'
│ }
├── [2] {
│   event: 'section_view',
│   section_id: 'about',
│   section_title: 'About',
│   timestamp: '2025-02-07T10:30:55.789Z'
│ }
└── [...more events]
```

---

## 3. Event Type Mapping

```
┌─────────────────────────────────────────────────────────┐
│           USER ACTIONS & EVENT MAPPING                  │
├─────────────────────────────────────────────────────────┤
│                                                           │
│ Click Navigation Link                                    │
│ └─→ EVENT: navigation_click                             │
│     ├─ nav_text: "About"                               │
│     ├─ nav_link: "#about"                              │
│     └─ timestamp: ISO-8601                             │
│                                                           │
│ Scroll to Section                                       │
│ └─→ EVENT: section_view                                │
│     ├─ section_id: "about"                             │
│     ├─ section_title: "About"                          │
│     └─ timestamp: ISO-8601                             │
│                                                           │
│ Download Resume                                         │
│ └─→ EVENT: file_download ⭐ CONVERSION                 │
│     ├─ file_name: "Resume - Saurabh..."               │
│     ├─ file_url: "resume/*.pdf"                        │
│     ├─ download_type: "resume"                         │
│     └─ timestamp: ISO-8601                             │
│                                                           │
│ Scroll Page (25%, 50%, 75%, 100%)                      │
│ └─→ EVENT: scroll_depth                                │
│     ├─ scroll_depth_threshold: "50%"                   │
│     └─ timestamp: ISO-8601                             │
│                                                           │
│ Click Email/Phone Link                                  │
│ └─→ EVENT: contact_initiated ⭐ CONVERSION            │
│     ├─ contact_type: "email" / "phone"                │
│     ├─ email/phone: actual value                       │
│     └─ timestamp: ISO-8601                             │
│                                                           │
│ Click Project Link                                      │
│ └─→ EVENT: portfolio_click ⭐ CONVERSION              │
│     ├─ project_name: "ChefMate"                        │
│     ├─ project_url: "github.com/..."                   │
│     ├─ click_type: "project_link"                      │
│     └─ timestamp: ISO-8601                             │
│                                                           │
│ Click Project Preview                                   │
│ └─→ EVENT: portfolio_view                              │
│     ├─ project_name: "ChefMate"                        │
│     ├─ view_type: "modal_preview"                      │
│     └─ timestamp: ISO-8601                             │
│                                                           │
│ Click Social Link (GitHub/LinkedIn/etc)                │
│ └─→ EVENT: social_link_click ⭐ CONVERSION           │
│     ├─ platform: "GitHub"                              │
│     ├─ url: "github.com/..."                           │
│     └─ timestamp: ISO-8601                             │
│                                                           │
└─────────────────────────────────────────────────────────┘
```

---

## 4. GTM Container Architecture

```
┌──────────────────────────────────────────────┐
│  GOOGLE TAG MANAGER (GTM-KP2GS6B6)           │
├──────────────────────────────────────────────┤
│                                               │
│  DATA LAYER INPUT                            │
│  └─→ window.dataLayer.push({...})           │
│                                               │
│  ┌────────────────────────────────────┐      │
│  │  TRIGGERS (9 Total)                │      │
│  ├────────────────────────────────────┤      │
│  │ ✓ All Pages (Pageview)            │      │
│  │ ✓ navigation_click (Custom Event)  │      │
│  │ ✓ section_view (Custom Event)      │      │
│  │ ✓ file_download (Custom Event)     │      │
│  │ ✓ scroll_depth (Custom Event)      │      │
│  │ ✓ contact_initiated (Custom)       │      │
│  │ ✓ portfolio_click (Custom Event)    │      │
│  │ ✓ portfolio_view (Custom Event)     │      │
│  │ ✓ social_link_click (Custom)       │      │
│  └────────────────────────────────────┘      │
│           ↓           ↓           ↓           │
│  ┌────────────────────────────────────┐      │
│  │  TAGS (9 GA4 Event Tags)          │      │
│  ├────────────────────────────────────┤      │
│  │ 1. GA4 - Page View                │      │
│  │ 2. GA4 - Navigation Click         │      │
│  │ 3. GA4 - Section View             │      │
│  │ 4. GA4 - Resume Download          │      │
│  │ 5. GA4 - Scroll Depth             │      │
│  │ 6. GA4 - Contact Initiated        │      │
│  │ 7. GA4 - Portfolio Click          │      │
│  │ 8. GA4 - Portfolio View           │      │
│  │ 9. GA4 - Social Link Click        │      │
│  └────────────────────────────────────┘      │
│           ↓           ↓           ↓           │
│  GA4 MEASUREMENT PROTOCOL OUTPUT              │
│  └─→ Measurement ID: G-HJBS8KBJJF           │
│                                               │
└──────────────────────────────────────────────┘
```

---

## 5. GA4 Event Processing Pipeline

```
┌──────────────────────────────────────────────────┐
│  GOOGLE ANALYTICS 4 (G-HJBS8KBJJF)              │
├──────────────────────────────────────────────────┤
│                                                   │
│  EVENT RECEIVED                                  │
│  └─→ {event: "navigation_click", ...}           │
│                                                   │
│  VALIDATION LAYER                               │
│  ├─ Event name check ✓                          │
│  ├─ Parameter validation ✓                      │
│  ├─ Timestamp validation ✓                      │
│  └─ User identification ✓                       │
│                                                   │
│  ENHANCEMENT LAYER                              │
│  ├─ Auto-capture: page_location                │
│  ├─ Auto-capture: page_title                   │
│  ├─ Auto-capture: session_id                   │
│  └─ Auto-capture: user_id                      │
│                                                   │
│  REAL-TIME PROCESSING                          │
│  ├─ Active Users updated                       │
│  ├─ Event count incremented                    │
│  ├─ Real-time report updated                   │
│  └─ Latency: 1-2 seconds                       │
│                                                   │
│  CONVERSION CHECKING                           │
│  ├─ Is this file_download? → Resume_Download   │
│  ├─ Is this contact_initiated? → Contact_Init  │
│  ├─ Is this portfolio_click? → Portfolio_Eng   │
│  ├─ Is this social_link_click? → Social_Out    │
│  └─ Is scroll_depth >= 75%? → High_Engagement │
│                                                   │
│  LONG-TERM STORAGE                             │
│  ├─ Daily processing (full events)              │
│  ├─ 4-month data retention                      │
│  ├─ Aggregated reports available                │
│  └─ Latency: 24-48 hours                       │
│                                                   │
└──────────────────────────────────────────────────┘
```

---

## 6. Conversion Goal Hierarchy

```
                    ALL USERS
                        ↓
        ┌───────────────┬───────────────┬───────────────┐
        ↓               ↓               ↓               ↓
    PAGE VIEWS    PORTFOLIO VIEWS  SECTION VIEWS  SCROLL DEPTH
      100%             60%             45%            35%
        ↓               ↓               ↓               ↓
        ├─→ social_link_click
        │   (20% of users)
        │   └─→ CONVERSION: Social_Outreach
        │
        ├─→ portfolio_click
        │   (15% of users)
        │   └─→ CONVERSION: Portfolio_Engagement
        │
        ├─→ file_download
        │   (8% of users)
        │   └─→ CONVERSION: Resume_Download ⭐ HIGH VALUE
        │
        └─→ contact_initiated
            (3% of users)
            └─→ CONVERSION: Contact_Initiated ⭐⭐ HIGHEST VALUE


CONVERSION FUNNEL (Example):
100 Users Land
    ↓
60 View Portfolio (60%)
    ↓
15 Click Project (15%)
    ↓
8 Download Resume (8%)
    ↓
3 Contact (3%) ⭐ FINAL CONVERSION
```

---

## 7. Data Flow Diagram (End-to-End)

```
┌─────────────────────────────────────────────────────────┐
│  USER INTERACTS WITH WEBSITE                            │
│  (Click, Scroll, Download, etc.)                        │
└──────────────────┬──────────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────────┐
│  JAVASCRIPT EVENT LISTENER                              │
│  (Attached to DOM elements & scroll events)             │
└──────────────────┬──────────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────────┐
│  DATA LAYER PUSH                                        │
│  window.dataLayer.push({                                │
│    event: '...',                                        │
│    param1: '...',                                       │
│    param2: '...',                                       │
│    timestamp: ISO-8601                                  │
│  })                                                     │
└──────────────────┬──────────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────────┐
│  GOOGLE TAG MANAGER                                     │
│  • Intercepts dataLayer push                            │
│  • Checks triggers                                      │
│  • Fires matching tags                                  │
└──────────────────┬──────────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────────┐
│  GA4 MEASUREMENT PROTOCOL                               │
│  • Sends event to GA4                                   │
│  • Includes all parameters                              │
│  • Includes auto-captured data                          │
└──────────────────┬──────────────────────────────────────┘
                   ↓
┌─────────────────────────────────────────────────────────┐
│  GOOGLE ANALYTICS 4 (Real-time)                         │
│  • Updates active users (1-2s)                          │
│  • Displays event in real-time report                   │
│  • Checks conversion conditions                         │
└──────────────────┬──────────────────────────────────────┘
                   ↓
        ┌──────────┴──────────┐
        ↓                     ↓
┌──────────────────┐  ┌──────────────────┐
│ REAL-TIME VIEW   │  │ LONG-TERM VIEW   │
│ (1-30 minutes)   │  │ (24-48 hours)    │
├──────────────────┤  ├──────────────────┤
│ • Active users   │  │ • Full data      │
│ • Live events    │  │ • Aggregated     │
│ • Conversion $   │  │ • Reports ready  │
└──────────────────┘  └──────────────────┘
        ↓                     ↓
    GTM Preview         Looker Studio
    (For testing)       (For analysis)
```

---

## 8. Implementation Checklist (Visual)

```
PHASE 1: CODE IMPLEMENTATION
✅ Data layer initialized
✅ Event tracking code added
✅ GTM script installed
✅ All 9 events configured

PHASE 2: GTM SETUP (USER ACTION REQUIRED)
□ Login to GTM container
□ Create 9 GA4 event tags
□ Configure 9 triggers
□ Test in preview mode
□ Verify all tags firing (Green)

PHASE 3: GA4 SETUP (USER ACTION REQUIRED)
□ Login to GA4 property
□ Enable 8 custom events
□ Create 5 conversion goals
□ Test real-time report
□ Verify conversions firing

PHASE 4: TESTING (USER ACTION REQUIRED)
□ Local data layer validation
□ GTM Preview mode testing
□ GA4 Real-time testing
□ Conversion verification
□ Parameter accuracy check

PHASE 5: REPORTING
□ Create Looker Studio dashboard
□ Set up automated reports
□ Create portfolio case study
□ Deploy to production
```

---

## 9. Event Parameter Reference Matrix

```
┌────────────────────────────────────────────────────────────────┐
│ EVENT NAME          │ KEY PARAMETERS          │ CONVERSION     │
├────────────────────────────────────────────────────────────────┤
│ page_view           │ page_title, page_path   │ NO             │
│ navigation_click    │ nav_text, nav_link      │ NO             │
│ section_view        │ section_id, title       │ NO             │
│ file_download       │ file_name, file_url     │ YES ⭐         │
│ scroll_depth        │ threshold (%)           │ YES (75%+)     │
│ contact_initiated   │ type, email/phone       │ YES ⭐⭐       │
│ portfolio_click     │ project_name, url       │ YES ⭐         │
│ portfolio_view      │ project_name, type      │ NO             │
│ social_link_click   │ platform, url           │ YES ⭐         │
└────────────────────────────────────────────────────────────────┘
```

---

## 10. Troubleshooting Decision Tree

```
EVENT NOT APPEARING IN GA4 REALTIME?
├─ Check Console for JavaScript Errors
│  ├─ YES → Fix error, reload page
│  └─ NO → Continue...
├─ Is event firing in GTM Preview?
│  ├─ NO → Check data layer push (console log)
│  │  ├─ Event not in data layer? → Check JS listeners
│  │  └─ Event in data layer? → Check GTM trigger
│  └─ YES → Continue...
├─ Is event appearing in GA4 Real-time?
│  ├─ NO → Wait 2-5 minutes, refresh
│  │  ├─ Still not there? → Check Measurement ID
│  │  └─ Appeared? → Continue...
│  └─ YES → ✅ Event working!
├─ Parameters missing in GA4?
│  ├─ Check data layer has parameter
│  └─ Add to GA4 Custom Definitions if missing

CONVERSION NOT FIRING?
├─ Is base event firing in GA4?
│  ├─ NO → First fix the base event
│  └─ YES → Continue...
├─ Is conversion enabled in GA4?
│  ├─ NO → Enable it
│  └─ YES → Continue...
├─ Is conversion name correct?
│  ├─ NO → Fix conversion event name match
│  └─ YES → Wait 24 hours for full processing

✅ ALL TESTS PASSING?
└─ Ready for Looker Studio dashboard
```

---

## 11. Timeline & Milestones

```
DAY 1: GTM Setup
├─ Morning: Create 9 GA4 tags
├─ Afternoon: Configure 9 triggers
├─ Evening: Test in preview mode

DAY 2: GA4 Setup
├─ Morning: Enable 8 custom events
├─ Afternoon: Create 5 conversions
├─ Evening: Verify real-time data

DAY 3: Testing & Validation
├─ Morning: Local validation
├─ Afternoon: GTM Preview testing
├─ Evening: GA4 Real-time testing

DAY 4: Data Collection
├─ Morning: Verify 24h data
├─ Afternoon: Run first reports
├─ Evening: Create dashboard

DAY 5+: Analysis & Optimization
├─ Create Looker Studio dashboards
├─ Set up automated reports
├─ Write portfolio case study
└─ Optimize tracking (if needed)
```

---

## 12. Success Metrics

```
TECHNICAL METRICS:
✓ 100% of events captured
✓ 0% dropped events
✓ 0% duplicate events
✓ 0 JavaScript errors
✓ Real-time latency: 1-2 seconds
✓ All parameters captured
✓ All conversions firing

DATA QUALITY METRICS:
✓ Event names: Consistent
✓ Parameter names: Consistent
✓ Timestamps: ISO 8601 format
✓ No null values
✓ Session tracking: Accurate
✓ User identification: Accurate

BUSINESS METRICS:
✓ Resume download rate: Trackable
✓ Contact rate: Trackable
✓ Engagement rate: Trackable
✓ Conversion funnel: Visible
✓ User journey: Analyzable
✓ Portfolio effectiveness: Measurable
```

---

**This document serves as a visual reference for the complete event tracking architecture and implementation flow.**
