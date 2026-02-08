# GA4 Conversion Goals Setup - Step by Step

## Accessing GA4 Conversion Settings

### Step 1: Log in to Google Analytics
1. Go to [Google Analytics](https://analytics.google.com)
2. Select your **Property**: "Portfolio Website"
3. Click on **Admin** (bottom left gear icon)

### Step 2: Navigate to Conversions
- In Admin panel, go to: **Data Collection and Modification** → **Events**
- OR: **Conversion** → **New Conversion Event**

---

## Creating Conversion Goals

### Conversion Goal 1: Resume Download ⭐ HIGH PRIORITY

**Navigation**: Admin → Conversions → New Conversion Event

**Configuration**:
```
Event Name: file_download
Conversion Name: Resume_Download
Description: Tracks resume file downloads
Icon: Download
Status: Enable
```

**Why This Matters**: 
- Shows intent to learn about you
- Indicates high engagement
- Potential lead indicator

---

### Conversion Goal 2: Contact Initiated ⭐ HIGH PRIORITY

**Navigation**: Admin → Conversions → New Conversion Event

**Configuration**:
```
Event Name: contact_initiated
Conversion Name: Contact_Initiated
Description: User attempted to contact (email or phone)
Icon: Contact
Status: Enable
```

**Why This Matters**: 
- Direct conversion goal
- Shows readiness to connect
- Most valuable action

---

### Conversion Goal 3: Portfolio Project Engagement ⭐ MEDIUM PRIORITY

**Navigation**: Admin → Conversions → New Conversion Event

**Configuration**:
```
Event Name: portfolio_click
Conversion Name: Portfolio_Engagement
Description: User clicked on project link (high intent)
Icon: Link
Status: Enable
```

**Why This Matters**: 
- Shows interest in specific projects
- Validates portfolio quality
- Helps identify popular projects

---

### Conversion Goal 4: Social Link Clicks ⭐ MEDIUM PRIORITY

**Navigation**: Admin → Conversions → New Conversion Event

**Configuration**:
```
Event Name: social_link_click
Conversion Name: Social_Outreach
Description: User clicked on social media links
Icon: Link
Status: Enable
```

**Why This Matters**: 
- Drives traffic to social profiles
- Increases social followers
- Shows trust in your presence

---

### Conversion Goal 5: High Engagement (75%+ Scroll) ⭐ LOW PRIORITY

**Navigation**: Admin → Conversions → New Conversion Event

**Configuration**:
```
Event Name: scroll_depth
Conversion Name: High_Engagement
Description: User scrolled 75% or more (high interest)
Icon: Scroll
Status: Enable
```

**Why This Matters**: 
- Engagement metric
- Shows content interest
- Helps optimize content

---

## Creating Custom Events in GA4

If events don't automatically register, manually create them:

**Navigation**: Admin → Data Collection and Modification → Events → Create Event

### Event 1: navigation_click
```
Event Name: navigation_click
Description: Navigation menu clicks
Parameters to Enable:
  ✓ nav_text
  ✓ nav_link
  ✓ timestamp
```

### Event 2: section_view
```
Event Name: section_view
Description: User viewed specific page section
Parameters to Enable:
  ✓ section_id
  ✓ section_title
  ✓ timestamp
```

### Event 3: portfolio_view
```
Event Name: portfolio_view
Description: User previewed project modal
Parameters to Enable:
  ✓ project_name
  ✓ view_type
  ✓ timestamp
```

---

## Event Parameter Definitions

### Parameters Reference

| Parameter | Event | Type | Example | Purpose |
|-----------|-------|------|---------|---------|
| nav_text | navigation_click | string | "About" | Which nav item clicked |
| nav_link | navigation_click | string | "#about" | Link destination |
| section_id | section_view | string | "about" | Section identifier |
| section_title | section_view | string | "About Me" | Display name |
| file_name | file_download | string | "Resume - Saurabh" | Downloaded file |
| file_url | file_download | string | "resume/*.pdf" | File path |
| download_type | file_download | string | "resume" | Category |
| project_name | portfolio_click | string | "ChefMate" | Project title |
| project_url | portfolio_click | string | "github.com/..." | Project link |
| click_type | portfolio_click | string | "project_link" | Click category |
| platform | social_link_click | string | "GitHub" | Social platform |
| url | social_link_click | string | "github.com/..." | Social profile URL |
| scroll_depth_threshold | scroll_depth | string | "50%" | Scroll percentage |
| contact_type | contact_initiated | string | "email" / "phone" | Contact method |
| email | contact_initiated | string | "user@gmail.com" | Email address |
| phone | contact_initiated | string | "+91 9503371603" | Phone number |
| timestamp | all | timestamp | "2025-02-07T10:30:45Z" | Event time |

---

## Conversion Funnel Setup

### Create a Conversion Funnel: Contact Funnel
**Navigation**: Admin → Conversions → Create Conversion Funnel

**Funnel Name**: Contact_Conversion_Funnel

**Funnel Steps**:
```
Step 1: Page View (Entry)
  Condition: page_path contains "index.html"

Step 2: Portfolio View (Interest)
  Event: portfolio_view

Step 3: Contact Initiated (Conversion)
  Event: contact_initiated
```

---

## Advanced: Create Custom Metric for Engagement Score

**Navigation**: Admin → Custom Definitions → Create Metric

```
Metric Name: Engagement_Score
Description: Overall engagement scoring
Scope: User
Formula: 
  (scroll_depth_event_count * 1) + 
  (portfolio_click_count * 5) + 
  (contact_initiated_count * 100)
```

---

## Verification Checklist

After setting up conversions, verify:

**✓ Conversion Events Active**
- [ ] Resume_Download showing in Conversions list
- [ ] Contact_Initiated showing in Conversions list
- [ ] Portfolio_Engagement showing in Conversions list
- [ ] Social_Outreach showing in Conversions list

**✓ Events Recording Data**
- [ ] Go to Reports → Realtime
- [ ] Perform actions on website
- [ ] See events appear with correct names
- [ ] See event counts incrementing

**✓ Parameters Visible**
- [ ] Go to Realtime → Event
- [ ] Click event to expand
- [ ] See all parameters displayed correctly
- [ ] No "null" or "undefined" values

**✓ Conversions Recording**
- [ ] Go to Reports → Realtime
- [ ] Conversions counter incrementing when actions taken
- [ ] Conversion Rate showing correct calculation

---

## Testing Each Conversion

### Test 1: Resume Download Conversion
1. Click "Download Resume" button
2. Check GA4 Realtime → file_download event appears
3. Check Conversions → Resume_Download counter increments
4. Expected: Count +1

### Test 2: Contact Initiated Conversion
1. Click "Say Hello" or email link
2. Check GA4 Realtime → contact_initiated event appears
3. Check Conversions → Contact_Initiated counter increments
4. Expected: Count +1

### Test 3: Portfolio Click Conversion
1. Click any GitHub project link
2. Check GA4 Realtime → portfolio_click event appears
3. Check Conversions → Portfolio_Engagement counter increments
4. Expected: Count +1

### Test 4: Social Link Conversion
1. Click social media link (GitHub, LinkedIn, etc.)
2. Check GA4 Realtime → social_link_click event appears
3. Check Conversions → Social_Outreach counter increments
4. Expected: Count +1

---

## Troubleshooting Conversion Setup

### Issue: Conversions Not Recording
**Solution**:
1. Verify event name matches exactly (case-sensitive)
2. Check event is firing in Realtime view
3. Wait 1-2 minutes, GA4 has processing delay
4. Verify conversion event is marked as "Active"

### Issue: Parameters Not Showing
**Solution**:
1. Go to Admin → Custom Definitions
2. Search for missing parameter
3. If not found, add manually:
   - Parameter name: (exact name from data layer)
   - Scope: Event
   - Description: (optional)
4. Wait 24 hours for full processing

### Issue: Zero Conversion Rate
**Solution**:
1. Verify events are firing (check Realtime)
2. Verify users are actually performing conversions
3. Check conversion events are enabled (not paused)
4. Verify measurement ID is correct: G-HJBS8KBJJF

### Issue: Only Some Parameters Showing
**Solution**:
1. Parameter names are case-sensitive
2. Must match data layer exactly
3. Check for typos (e.g., "project_name" vs "projectName")
4. Add parameter in Custom Definitions if missing

---

## Next Steps

After verifying conversions:
1. ✅ Enable UTM tracking for external referrals
2. ✅ Create Looker Studio dashboard
3. ✅ Set up email alerts for conversions
4. ✅ Create audience segments
5. ✅ Schedule automated reports

---

## GA4 Property Information

| Setting | Value |
|---------|-------|
| Property Name | Portfolio Website |
| Measurement ID | G-HJBS8KBJJF |
| Region | India |
| Timezone | Asia/Kolkata (IST) |
| Currency | INR |

---

## Support Resources

- [GA4 Setup Guide](https://support.google.com/analytics/answer/9304153)
- [Create & Manage Conversions](https://support.google.com/analytics/answer/12188663)
- [Custom Events in GA4](https://support.google.com/analytics/answer/9267744)
- [Debug View](https://support.google.com/analytics/answer/7201382)
