# Complete Testing & Validation Checklist

## Pre-Testing Setup

### ✅ Prerequisites
- [ ] Website deployed and live
- [ ] GTM container ID: GTM-KP2GS6B6 ✓
- [ ] GA4 Measurement ID: G-HJBS8KBJJF ✓
- [ ] Chrome browser with Google Tag Manager Assistant extension
- [ ] Google Analytics account access
- [ ] GTM container access

---

## Phase 1: Data Layer Validation (LOCAL)

### Step 1: Open Developer Console
```
Browser: Chrome
Action: Press F12 or Right-click → Inspect
Go to: Console tab
```

### Step 2: Load Data Layer Validator
```javascript
// Copy-paste in console:
// The validator is in data-layer-validator.html
// Or run these commands directly:

// Check data layer exists
> window.dataLayer
> Expected: Array of objects with 'event' property

// Check initial page_view event
> window.dataLayer[0]
> Expected: { event: 'page_view', page_title: '...', ... }
```

### Step 3: Test Data Layer Events Manually

**Test Navigation Click Event**:
```javascript
// In Console:
console.log('Testing navigation_click...');
// Then click "About" link in navigation
// Expected in Console:
// [navigation_click] { 
//   event: 'navigation_click',
//   nav_text: 'About',
//   nav_link: '#about',
//   timestamp: '2025-02-07T10:30:45.123Z'
// }
```

**Validation Result**:
- [ ] Event fired
- [ ] nav_text captured
- [ ] nav_link captured
- [ ] timestamp in ISO format
- [ ] No null/undefined values

---

### Step 4: Test All Event Types

#### Navigation Click Event ✓
```
Action: Click navigation link (About)
Check: 
  - nav_text = "About" ✓
  - nav_link = "#about" ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

#### Section View Event ✓
```
Action: Scroll to "About" section
Check:
  - section_id = "about" ✓
  - section_title = "About" ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

#### File Download Event ✓
```
Action: Click "Download Resume" button
Check:
  - file_name = "Resume - Saurabh Rajendra Dubey" ✓
  - file_url = "resume/resume_saurabh_rajendra_dubey.pdf" ✓
  - download_type = "resume" ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

#### Scroll Depth Event ✓
```
Action: Scroll page to 25%, 50%, 75%, 100%
Check (for each threshold):
  - scroll_depth_threshold = "25%" / "50%" / "75%" / "100%" ✓
  - timestamp = ISO format ✓
  - Event fires only once per threshold ✓
Status: [ ] Pass [ ] Fail
```

#### Contact Initiated Event (Email) ✓
```
Action: Click email link or "Say Hello" button
Check:
  - contact_type = "email" ✓
  - email = "dubeysaurabhrajendra@gmail.com" ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

#### Contact Initiated Event (Phone) ✓
```
Action: Click phone link
Check:
  - contact_type = "phone" ✓
  - phone = "+91 9503371603" ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

#### Portfolio Click Event ✓
```
Action: Click GitHub link on any project
Check:
  - project_name = "ChefMate" / "PaperPulse" / etc. ✓
  - project_url = GitHub URL ✓
  - click_type = "project_link" ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

#### Portfolio View Event ✓
```
Action: Click on project image/modal preview
Check:
  - project_name = Project name ✓
  - view_type = "modal_preview" ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

#### Social Link Click Event ✓
```
Action: Click GitHub / LinkedIn / Instagram link
Check:
  - platform = "GitHub" / "LinkedIn" / "Instagram" ✓
  - url = Social profile URL ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

#### Page View Event ✓
```
Action: Page loads automatically
Check:
  - event = "page_view" ✓
  - page_title = "Saurabh Rajendra" ✓
  - page_path = "/" ✓
  - timestamp = ISO format ✓
Status: [ ] Pass [ ] Fail
```

---

## Phase 2: GTM Preview Mode Testing

### Step 1: Enable GTM Preview Mode

**In GTM Container**:
1. Go to [Google Tag Manager](https://tagmanager.google.com)
2. Select Container: GTM-KP2GS6B6
3. Click **Preview** button (top-right)
4. A dialog appears with preview URL
5. Copy the URL

**On Your Website**:
1. Open new tab with your website
2. Paste preview URL
3. GTM debug panel appears at bottom-left

### Step 2: Verify Tags in GTM Preview

**Opening GTM Debug Panel**:
- Look for gray panel at bottom-left of browser
- It should show:
  - "Google Tag Manager: GTM-KP2GS6B6"
  - Tabs: Summary, Tags, Triggers, Variables, Data Layer

### Step 3: Test Each Tag in Preview Mode

**Navigation Click Tag**:
```
Action: Click "About" link
GTM Debug Panel:
  Go to: Tags tab
  Look for: GA4 - Navigation Click (Green ✓)
  Status: Should show "Fired"
  Data: Should show nav_text, nav_link
Result: [ ] Pass [ ] Fail
```

**Section View Tag**:
```
Action: Scroll to section (About/Works/Contact)
GTM Debug Panel:
  Go to: Tags tab
  Look for: GA4 - Section View (Green ✓)
  Status: Should show "Fired"
  Data: Should show section_id, section_title
Result: [ ] Pass [ ] Fail
```

**Resume Download Tag**:
```
Action: Click "Download Resume"
GTM Debug Panel:
  Go to: Tags tab
  Look for: GA4 - Resume Download (Green ✓)
  Status: Should show "Fired"
  Data: Should show file_name, file_url, download_type
Result: [ ] Pass [ ] Fail
```

**Scroll Depth Tag**:
```
Action: Scroll page slowly watching debug panel
GTM Debug Panel:
  Go to: Tags tab
  Look for: GA4 - Scroll Depth (Green ✓)
  Status: Should fire at 25%, 50%, 75%, 100%
  Data: Should show scroll_depth_threshold
Result: [ ] Pass [ ] Fail
```

**Contact Tag**:
```
Action: Click email or phone link
GTM Debug Panel:
  Go to: Tags tab
  Look for: GA4 - Contact Initiated (Green ✓)
  Status: Should show "Fired"
  Data: Should show contact_type, email/phone
Result: [ ] Pass [ ] Fail
```

**Portfolio Click Tag**:
```
Action: Click project GitHub link
GTM Debug Panel:
  Go to: Tags tab
  Look for: GA4 - Portfolio Click (Green ✓)
  Status: Should show "Fired"
  Data: Should show project_name, project_url
Result: [ ] Pass [ ] Fail
```

**Social Click Tag**:
```
Action: Click GitHub/LinkedIn/Instagram link
GTM Debug Panel:
  Go to: Tags tab
  Look for: GA4 - Social Link Click (Green ✓)
  Status: Should show "Fired"
  Data: Should show platform, url
Result: [ ] Pass [ ] Fail
```

### Step 4: Check Data Layer in GTM Preview

**View Data Layer Tab**:
1. In GTM Debug Panel, click **Data Layer** tab
2. You should see:
   - Initial page_view event
   - All custom events as you perform actions

**Sample Data Layer Content**:
```json
[
  {
    "event": "page_view",
    "page_title": "Saurabh Rajendra",
    "page_path": "/",
    "timestamp": "2025-02-07T10:30:45.123Z"
  },
  {
    "event": "navigation_click",
    "nav_text": "About",
    "nav_link": "#about",
    "timestamp": "2025-02-07T10:30:50.456Z"
  },
  ...
]
```

**Verification**:
- [ ] Data Layer tab shows events
- [ ] Events appear as you perform actions
- [ ] All parameters visible
- [ ] Timestamps are in ISO format
- [ ] No "undefined" or "null" values

---

## Phase 3: GA4 Real-Time Validation

### Step 1: Open GA4 Real-Time Report

1. Go to [Google Analytics](https://analytics.google.com)
2. Select Property: Portfolio Website
3. Go to **Reports** (left menu)
4. Click **Realtime** (top option)
5. Keep this open while testing

### Step 2: Verify Page View in Real-Time

```
GA4 Realtime:
  Metric: Active Users
  Should show: 1 (your session)
  
  Event: page_view
  Should appear in event list
  Click event to expand
  
  Parameters:
    - page_location ✓
    - page_title ✓
    - session_id ✓
    
Status: [ ] Pass [ ] Fail
```

### Step 3: Test Each Event in Real-Time

**Navigation Click in Real-Time**:
```
Action: Click "About" link (in GTM Preview mode)
GA4 Realtime - Events:
  Look for: navigation_click
  Event count: +1
  Parameters shown:
    - nav_text: "About" ✓
    - nav_link: "#about" ✓
    - timestamp: ISO format ✓
Status: [ ] Pass [ ] Fail
Timing: Should appear within 1-2 seconds
```

**Section View in Real-Time**:
```
Action: Scroll to section
GA4 Realtime - Events:
  Look for: section_view
  Event count: +1
  Parameters shown:
    - section_id ✓
    - section_title ✓
    - timestamp ✓
Status: [ ] Pass [ ] Fail
```

**File Download in Real-Time**:
```
Action: Click resume download
GA4 Realtime - Events:
  Look for: file_download
  Event count: +1
  Parameters shown:
    - file_name ✓
    - file_url ✓
    - download_type ✓
    - timestamp ✓
Status: [ ] Pass [ ] Fail
```

**Scroll Depth in Real-Time**:
```
Action: Scroll to each threshold
GA4 Realtime - Events:
  Look for: scroll_depth (multiple)
  Events at: 25%, 50%, 75%, 100%
  Parameters shown:
    - scroll_depth_threshold ✓
    - timestamp ✓
Status: [ ] Pass [ ] Fail
```

**Contact Initiated in Real-Time**:
```
Action: Click email/phone link
GA4 Realtime - Events:
  Look for: contact_initiated
  Event count: +1
  Parameters shown:
    - contact_type ✓
    - email or phone ✓
    - timestamp ✓
Status: [ ] Pass [ ] Fail
```

**Portfolio Click in Real-Time**:
```
Action: Click project link
GA4 Realtime - Events:
  Look for: portfolio_click
  Event count: +1
  Parameters shown:
    - project_name ✓
    - project_url ✓
    - click_type ✓
Status: [ ] Pass [ ] Fail
```

**Social Link in Real-Time**:
```
Action: Click GitHub/LinkedIn/etc
GA4 Realtime - Events:
  Look for: social_link_click
  Event count: +1
  Parameters shown:
    - platform ✓
    - url ✓
    - timestamp ✓
Status: [ ] Pass [ ] Fail
```

---

## Phase 4: Conversion Goals Validation

### Step 1: Check Conversions in GA4

1. Go to **Admin** → **Conversions**
2. Verify these conversions exist:
   - [ ] Resume_Download
   - [ ] Contact_Initiated
   - [ ] Portfolio_Engagement
   - [ ] Social_Outreach
   - [ ] High_Engagement_Scroll

### Step 2: Test Each Conversion

**Resume Download Conversion**:
```
Action: Click "Download Resume"
Wait: 1-2 seconds for GA4 to process
GA4 Location: Reports → Realtime → Conversions
Expected:
  - file_download event appears
  - Resume_Download conversion counter +1
Timing: Should update within 2-5 seconds
Status: [ ] Pass [ ] Fail
```

**Contact Initiated Conversion**:
```
Action: Click "Say Hello" button
Wait: 1-2 seconds
GA4 Location: Reports → Realtime → Conversions
Expected:
  - contact_initiated event appears
  - Contact_Initiated conversion counter +1
Status: [ ] Pass [ ] Fail
```

**Portfolio Engagement Conversion**:
```
Action: Click project GitHub link
Wait: 1-2 seconds
GA4 Location: Reports → Realtime → Conversions
Expected:
  - portfolio_click event appears
  - Portfolio_Engagement conversion counter +1
Status: [ ] Pass [ ] Fail
```

**Social Outreach Conversion**:
```
Action: Click GitHub/LinkedIn/etc link
Wait: 1-2 seconds
GA4 Location: Reports → Realtime → Conversions
Expected:
  - social_link_click event appears
  - Social_Outreach conversion counter +1
Status: [ ] Pass [ ] Fail
```

---

## Phase 5: Parameter Accuracy Validation

### Data Integrity Checks

For each event captured, verify:

| Parameter | Check | Pass/Fail |
|-----------|-------|-----------|
| Event names | Exact match (case-sensitive) | [ ] |
| Parameter names | Exact match (case-sensitive) | [ ] |
| Timestamps | ISO 8601 format | [ ] |
| Values | No "null" or "undefined" | [ ] |
| URLs | Complete and valid | [ ] |
| Text fields | No HTML encoding issues | [ ] |

### Event Accuracy Matrix

```
Event Type          | Data Layer | GTM Preview | GA4 Realtime | Conversion
navigation_click    | [ ] Pass    | [ ] Pass    | [ ] Pass     | N/A
section_view        | [ ] Pass    | [ ] Pass    | [ ] Pass     | N/A
file_download       | [ ] Pass    | [ ] Pass    | [ ] Pass     | [ ] Pass
scroll_depth        | [ ] Pass    | [ ] Pass    | [ ] Pass     | [ ] Pass
contact_initiated   | [ ] Pass    | [ ] Pass    | [ ] Pass     | [ ] Pass
portfolio_click     | [ ] Pass    | [ ] Pass    | [ ] Pass     | [ ] Pass
portfolio_view      | [ ] Pass    | [ ] Pass    | [ ] Pass     | N/A
social_link_click   | [ ] Pass    | [ ] Pass    | [ ] Pass     | [ ] Pass
page_view           | [ ] Pass    | [ ] Pass    | [ ] Pass     | N/A
```

---

## Final Validation Summary

### Critical Tests (Must Pass)
- [ ] Data layer captures all events
- [ ] GTM Preview shows all tags firing (green)
- [ ] GA4 Realtime shows all events
- [ ] Conversions fire correctly
- [ ] No JavaScript errors in console

### Quality Tests (Should Pass)
- [ ] All parameters present and accurate
- [ ] Timestamps are consistent
- [ ] No null/undefined values
- [ ] Event counts are logical
- [ ] User session ID tracked consistently

### Performance Tests
- [ ] Events fire within 1-2 seconds
- [ ] No page performance degradation
- [ ] No console warnings/errors
- [ ] Tracking doesn't block page load

---

## Troubleshooting Reference

### Issue: Event not firing in GTM Preview
**Solution**:
- [ ] Check trigger conditions in GTM
- [ ] Verify custom event name matches data layer exactly
- [ ] Check data layer is pushing the event (console.log)
- [ ] Refresh GTM Preview tab

### Issue: Event appears in GTM but not GA4
**Solution**:
- [ ] Wait 2-5 minutes for GA4 processing
- [ ] Check GA4 Measurement ID is correct
- [ ] Verify GA4 tag is in GTM and firing
- [ ] Check for ad blockers blocking GA4

### Issue: Conversion not firing
**Solution**:
- [ ] Check event is firing in GA4 Realtime
- [ ] Verify conversion event name matches exactly
- [ ] Check conversion is enabled (not paused)
- [ ] Wait 24 hours for first data processing

### Issue: Parameters showing as (not set)
**Solution**:
- [ ] Check parameter name matches data layer exactly (case-sensitive)
- [ ] Verify parameter is being pushed in data layer
- [ ] Add parameter to GA4 Custom Definitions
- [ ] Wait 24 hours for processing

---

## Sign-Off

**Testing Date**: _______________
**Tested By**: _______________
**Overall Result**: [ ] PASS [ ] FAIL

**If FAIL, describe issues**:
```
_________________________________
_________________________________
_________________________________
```

**Next Steps After Passing**:
1. Exit GTM Preview mode
2. Create Looker Studio dashboard
3. Set up automated reports
4. Create portfolio case study
5. Deploy to production
