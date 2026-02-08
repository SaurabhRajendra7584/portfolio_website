# GTM & GA4 Setup Guide - Complete Configuration

## Table of Contents
1. [GTM Container Setup](#gtm-container-setup)
2. [GA4 Event Configuration](#ga4-event-configuration)
3. [Conversion Goals](#conversion-goals)
4. [Testing & Validation](#testing--validation)

---

## GTM Container Setup

### GTM Account Details
- **Container ID**: GTM-KP2GS6B6
- **Container Type**: Web

### Required Tags (Create These in GTM)

#### Tag 1: GA4 Event - Page View
**Name**: GA4 - Page View
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: page_view
**Trigger**: All Pages (Pageview)

#### Tag 2: GA4 Event - Navigation Click
**Name**: GA4 - Navigation Click
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: navigation_click
**Event Parameters**:
- nav_text: {{nav_text}}
- nav_link: {{nav_link}}
- timestamp: {{timestamp}}

**Trigger Name**: Navigation Click Trigger
**Trigger Type**: Custom Event
**Event Name**: navigation_click

#### Tag 3: GA4 Event - Section View
**Name**: GA4 - Section View
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: section_view
**Event Parameters**:
- section_id: {{section_id}}
- section_title: {{section_title}}
- timestamp: {{timestamp}}

**Trigger Name**: Section View Trigger
**Trigger Type**: Custom Event
**Event Name**: section_view

#### Tag 4: GA4 Event - File Download (Resume)
**Name**: GA4 - Resume Download
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: file_download
**Event Parameters**:
- file_name: {{file_name}}
- file_url: {{file_url}}
- download_type: {{download_type}}
- timestamp: {{timestamp}}

**Trigger Name**: Resume Download Trigger
**Trigger Type**: Custom Event
**Event Name**: file_download

#### Tag 5: GA4 Event - Scroll Depth
**Name**: GA4 - Scroll Depth
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: scroll_depth
**Event Parameters**:
- scroll_depth_threshold: {{scroll_depth_threshold}}
- timestamp: {{timestamp}}

**Trigger Name**: Scroll Depth Trigger
**Trigger Type**: Custom Event
**Event Name**: scroll_depth

#### Tag 6: GA4 Event - Contact Initiated
**Name**: GA4 - Contact Initiated
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: contact_initiated
**Event Parameters**:
- contact_type: {{contact_type}}
- email: {{email}}
- phone: {{phone}}
- timestamp: {{timestamp}}

**Trigger Name**: Contact Initiated Trigger
**Trigger Type**: Custom Event
**Event Name**: contact_initiated

#### Tag 7: GA4 Event - Portfolio Click
**Name**: GA4 - Portfolio Click
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: portfolio_click
**Event Parameters**:
- project_name: {{project_name}}
- project_url: {{project_url}}
- click_type: {{click_type}}
- timestamp: {{timestamp}}

**Trigger Name**: Portfolio Click Trigger
**Trigger Type**: Custom Event
**Event Name**: portfolio_click

#### Tag 8: GA4 Event - Portfolio View
**Name**: GA4 - Portfolio View
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: portfolio_view
**Event Parameters**:
- project_name: {{project_name}}
- view_type: {{view_type}}
- timestamp: {{timestamp}}

**Trigger Name**: Portfolio View Trigger
**Trigger Type**: Custom Event
**Event Name**: portfolio_view

#### Tag 9: GA4 Event - Social Link Click
**Name**: GA4 - Social Link Click
**Tag Type**: Google Analytics: GA4 Event
**Measurement ID**: G-HJBS8KBJJF
**Event Name**: social_link_click
**Event Parameters**:
- platform: {{platform}}
- url: {{url}}
- timestamp: {{timestamp}}

**Trigger Name**: Social Link Click Trigger
**Trigger Type**: Custom Event
**Event Name**: social_link_click

---

## GA4 Event Configuration

### Login to GA4
1. Go to [Google Analytics](https://analytics.google.com)
2. Select Property: Portfolio Website
3. Navigate to: Admin → Events

### Create Custom Events in GA4

#### Event 1: navigation_click
- **Event Name**: navigation_click
- **Event Parameters to Enable**:
  - nav_text
  - nav_link
  - timestamp

#### Event 2: section_view
- **Event Name**: section_view
- **Event Parameters to Enable**:
  - section_id
  - section_title
  - timestamp

#### Event 3: file_download
- **Event Name**: file_download (May auto-enable)
- **Event Parameters to Enable**:
  - file_name
  - file_url
  - download_type
  - timestamp

#### Event 4: scroll_depth
- **Event Name**: scroll_depth
- **Event Parameters to Enable**:
  - scroll_depth_threshold
  - timestamp

#### Event 5: contact_initiated
- **Event Name**: contact_initiated
- **Event Parameters to Enable**:
  - contact_type
  - email
  - phone
  - timestamp

#### Event 6: portfolio_click
- **Event Name**: portfolio_click
- **Event Parameters to Enable**:
  - project_name
  - project_url
  - click_type
  - timestamp

#### Event 7: portfolio_view
- **Event Name**: portfolio_view
- **Event Parameters to Enable**:
  - project_name
  - view_type
  - timestamp

#### Event 8: social_link_click
- **Event Name**: social_link_click
- **Event Parameters to Enable**:
  - platform
  - url
  - timestamp

---

## Conversion Goals

### Setup Conversion Goals in GA4

**Path**: Admin → Conversions → New Conversion Event

#### Conversion 1: Resume Download
- **Event Name**: file_download
- **Conversion Name**: Resume_Download
- **Description**: Tracks when users download the resume
- **Icon**: Download

#### Conversion 2: Contact Initiated
- **Event Name**: contact_initiated
- **Conversion Name**: Contact_Initiated
- **Description**: Tracks email or phone contact attempts
- **Icon**: Contact

#### Conversion 3: Portfolio Project Clicks
- **Event Name**: portfolio_click
- **Conversion Name**: Portfolio_Engagement
- **Description**: Tracks project link clicks (high intent)
- **Icon**: Click

#### Conversion 4: Social Engagement
- **Event Name**: social_link_click
- **Conversion Name**: Social_Link_Click
- **Description**: Tracks outbound social link clicks
- **Icon**: Link

#### Conversion 5: High Engagement (Scroll 75%+)
- **Event Name**: scroll_depth
- **Filter**: scroll_depth_threshold == "75%" OR scroll_depth_threshold == "100%"
- **Conversion Name**: High_Engagement_Scroll
- **Description**: Tracks users who scroll 75% or more
- **Icon**: Scroll

---

## Testing & Validation

### Step 1: Enable GTM Debug Mode
1. Open your website in Chrome
2. Install "Google Tag Manager Assistant" extension
3. Click the extension icon
4. Go to Settings → Enable in Preview Mode
5. Copy the preview URL

### Step 2: GTM Preview Mode
1. In GTM Container, click **Preview**
2. Paste the preview URL in the dialog
3. Website loads in debug panel (bottom-left corner)
4. Check all tags firing correctly:
   - Green = tag fired
   - Red = tag failed
   - No color = trigger not matched

### Step 3: Check Data Layer
1. In GTM Preview Panel, go to **Data Layer** tab
2. Perform actions on website:
   - Click navigation links
   - Scroll page
   - Click resume download
   - Click social links
3. Verify **Data Layer** shows correct event data

### Step 4: GA4 Real-Time Report
1. In GA4, go to **Reports → Realtime**
2. Keep this open while testing website
3. You should see:
   - Page views appearing
   - Events appearing with correct event names
   - Event counts incrementing

### Step 5: Validate Each Event Type

**Test Navigation Click**:
1. Click on "About" link in navigation
2. GTM Preview: Should see `navigation_click` event
3. GA4 Realtime: Should see `navigation_click` event

**Test Section View**:
1. Scroll to "About" section
2. GTM Preview: Should see `section_view` event
3. GA4 Realtime: Should see `section_view` event

**Test Resume Download**:
1. Click "Download Resume" button
2. GTM Preview: Should see `file_download` event
3. GA4 Realtime: Should see `file_download` event

**Test Scroll Depth**:
1. Scroll page to 25%, 50%, 75%, 100%
2. GTM Preview: Should see `scroll_depth` events (one per threshold)
3. GA4 Realtime: Should see multiple `scroll_depth` events

**Test Portfolio Click**:
1. Click on any project link (GitHub icon)
2. GTM Preview: Should see `portfolio_click` event
3. GA4 Realtime: Should see `portfolio_click` event

**Test Contact Initiated**:
1. Click "Say Hello" or email link
2. GTM Preview: Should see `contact_initiated` event
3. GA4 Realtime: Should see `contact_initiated` event

**Test Social Link Click**:
1. Click any social link (GitHub, LinkedIn, etc.)
2. GTM Preview: Should see `social_link_click` event
3. GA4 Realtime: Should see `social_link_click` event

---

## Data Validation Checklist

### Each Event Should Contain:
- ✓ Event name (correct)
- ✓ Event parameters (all present)
- ✓ Timestamp (ISO format)
- ✓ User ID/Session ID (GA4 auto-generates)
- ✓ Page path/title (GA4 auto-captures)

### Parameter Validation Examples:

**navigation_click Event**:
```json
{
  "event": "navigation_click",
  "nav_text": "About",
  "nav_link": "#about",
  "timestamp": "2025-02-07T10:30:45.123Z"
}
```

**file_download Event**:
```json
{
  "event": "file_download",
  "file_name": "Resume - Saurabh Rajendra Dubey",
  "file_url": "resume/resume_saurabh_rajendra_dubey.pdf",
  "download_type": "resume",
  "timestamp": "2025-02-07T10:30:45.123Z"
}
```

**scroll_depth Event**:
```json
{
  "event": "scroll_depth",
  "scroll_depth_threshold": "50%",
  "timestamp": "2025-02-07T10:30:45.123Z"
}
```

---

## Troubleshooting

### Events Not Appearing in GA4 Real-time?
1. Check GTM Preview Mode → Data Layer tab
2. Verify events are firing in GTM
3. Wait 1-2 minutes for GA4 to update
4. Check timezone settings in GA4

### Event Parameters Not Showing?
1. Verify parameter names match exactly (case-sensitive)
2. Go to Admin → Custom Definitions
3. Add missing parameters manually
4. Wait 24 hours for full processing

### Zero Data in Real-time?
1. Verify GA4 Measurement ID is correct: G-HJBS8KBJJF
2. Check GTM container is live (not in preview)
3. Verify browser JavaScript is enabled
4. Check browser extensions not blocking tracking

### Tags Showing Red in GTM?
1. Check trigger conditions are correct
2. Verify Custom Event names match data layer events exactly
3. Check for JavaScript console errors (F12 → Console)

---

## Next Steps After Validation
1. ✓ All events firing in GTM Preview
2. ✓ All events appearing in GA4 Real-time
3. → Create Looker Studio Dashboard
4. → Set up automated reports
5. → Create portfolio case study
