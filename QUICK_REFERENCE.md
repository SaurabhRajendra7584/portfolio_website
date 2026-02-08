# Quick Reference Card - GTM & GA4 Setup

## 🎯 Quick Links

| Resource | URL |
|----------|-----|
| Google Tag Manager | https://tagmanager.google.com |
| Google Analytics 4 | https://analytics.google.com |
| GTM Container | GTM-KP2GS6B6 |
| GA4 Measurement ID | G-HJBS8KBJJF |

---

## 📋 Event Summary

| # | Event Name | Type | Conversion | Key Parameters |
|---|-----------|------|-----------|-----------------|
| 1 | page_view | Automatic | ❌ | page_title, page_path |
| 2 | navigation_click | Manual | ❌ | nav_text, nav_link |
| 3 | section_view | Manual | ❌ | section_id, section_title |
| 4 | file_download | Manual | ✅ Resume_Download | file_name, file_url, download_type |
| 5 | scroll_depth | Manual | ✅ High_Engagement | scroll_depth_threshold |
| 6 | contact_initiated | Manual | ✅ Contact_Initiated | contact_type, email/phone |
| 7 | portfolio_click | Manual | ✅ Portfolio_Engagement | project_name, project_url |
| 8 | portfolio_view | Manual | ❌ | project_name, view_type |
| 9 | social_link_click | Manual | ✅ Social_Outreach | platform, url |

---

## 🔧 GTM Setup Checklist

### Tags to Create (9 Total)
- [ ] GA4 - Page View
- [ ] GA4 - Navigation Click
- [ ] GA4 - Section View
- [ ] GA4 - Resume Download
- [ ] GA4 - Scroll Depth
- [ ] GA4 - Contact Initiated
- [ ] GA4 - Portfolio Click
- [ ] GA4 - Portfolio View
- [ ] GA4 - Social Link Click

### Triggers to Create (9 Total)
- [ ] All Pages (Pageview)
- [ ] Navigation Click Trigger (Custom Event)
- [ ] Section View Trigger (Custom Event)
- [ ] Resume Download Trigger (Custom Event)
- [ ] Scroll Depth Trigger (Custom Event)
- [ ] Contact Initiated Trigger (Custom Event)
- [ ] Portfolio Click Trigger (Custom Event)
- [ ] Portfolio View Trigger (Custom Event)
- [ ] Social Link Click Trigger (Custom Event)

---

## 📊 GA4 Setup Checklist

### Conversions to Create (5 Total)
- [ ] Resume_Download (file_download event)
- [ ] Contact_Initiated (contact_initiated event)
- [ ] Portfolio_Engagement (portfolio_click event)
- [ ] Social_Outreach (social_link_click event)
- [ ] High_Engagement (scroll_depth event, threshold 75%+)

### Custom Events to Enable (8 Total)
- [ ] navigation_click
- [ ] section_view
- [ ] portfolio_click
- [ ] portfolio_view
- [ ] social_link_click
- [ ] scroll_depth
- [ ] contact_initiated
- [ ] (file_download auto-enabled)

---

## 🧪 Testing Workflow

### Step 1: Local Validation (5 min)
```
1. Open Browser Console (F12)
2. Perform actions on website:
   - Click navigation
   - Scroll page
   - Download resume
   - Click social links
3. Verify events in console using DataLayerValidator
```

### Step 2: GTM Preview (10 min)
```
1. Enable GTM Preview Mode
2. Open debug panel (bottom-left)
3. Check Tags tab - all should be Green ✓
4. Check Data Layer tab - see all events
5. Verify no Red ✗ tags
```

### Step 3: GA4 Real-Time (10 min)
```
1. Open GA4 → Reports → Realtime
2. Keep GTM Preview running
3. Perform actions on website
4. Verify:
   - Events appearing in Realtime
   - Conversions counter incrementing
   - Parameters showing correctly
5. Wait 1-2 seconds between actions
```

### Step 4: Conversion Verification (5 min)
```
1. Go to GA4 → Admin → Conversions
2. For each conversion:
   - Verify it exists
   - Verify it's enabled (Active)
   - Verify it shows event count > 0
```

---

## ⚡ Quick Testing Commands

### Browser Console Commands
```javascript
// View all captured events
> DataLayerValidator.getAll()

// Validate event structure
> DataLayerValidator.validate()

// Get event counts
> DataLayerValidator.getEventCounts()

// Get specific event type
> DataLayerValidator.getEventsByName('navigation_click')

// Export as JSON
> DataLayerValidator.exportJSON()
```

---

## 🎯 Expected Results

### Data Layer (Local)
✓ 9 event types firing
✓ All parameters captured
✓ All timestamps in ISO format
✓ No null/undefined values

### GTM Preview Mode
✓ All 9 tags showing Green ✓
✓ No Red ✗ tags
✓ Data Layer tab shows events
✓ All parameters visible

### GA4 Real-Time
✓ Events appearing with 1-2s delay
✓ All 9 event types visible
✓ Conversions firing correctly
✓ Parameter values accurate

### Conversions Active
✓ 5 conversions showing in list
✓ Conversion counters incrementing
✓ Event counts > 0 for each

---

## ⚠️ Common Issues & Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| Events not in Console | JavaScript not running | Check console for errors, reload page |
| Red tags in GTM | Trigger not matching | Check trigger conditions, verify event name match |
| Events not in GA4 | Network/filter issue | Wait 2-5 min, check Measurement ID |
| Conversions at 0 | Event not firing | Verify event appears in GA4 Realtime first |
| Parameters missing | Name mismatch | Check case-sensitivity, add to Custom Definitions |
| Data showing (not set) | Parameter not in data layer | Add parameter or check data layer push |

---

## 📁 Documentation Files

| File | Purpose |
|------|---------|
| GTM_SETUP_GUIDE.md | Detailed GTM tag/trigger configuration |
| GA4_CONVERSION_SETUP.md | GA4 conversion & event setup |
| TESTING_VALIDATION_CHECKLIST.md | Complete testing procedures |
| data-layer-validator.html | Browser console validator script |
| index.html | Website with embedded tracking code |

---

## 🚀 Success Criteria (All Must Pass)

✓ Data layer captures all 9 event types
✓ GTM Preview shows all tags firing (Green)
✓ GA4 Realtime shows all 9 events
✓ All 5 conversions firing
✓ All parameters accurate
✓ No JavaScript errors
✓ No null/undefined values
✓ Timestamps consistent
✓ User session tracked

---

## 📝 Setup Checklist Summary

### Phase 1: Code Implementation ✅
- [x] Data layer initialized
- [x] Event tracking added to website
- [x] GTM script properly placed
- [x] All 9 event types implemented

### Phase 2: GTM Configuration (IN PROGRESS)
- [ ] 9 GA4 tags created
- [ ] 9 triggers configured
- [ ] All tags linked to GA4
- [ ] Preview mode testing

### Phase 3: GA4 Configuration (IN PROGRESS)
- [ ] 8 custom events enabled
- [ ] 5 conversions created
- [ ] Real-time testing completed
- [ ] Data validation passed

### Phase 4: Reporting & Dashboard
- [ ] Looker Studio connected
- [ ] Dashboard created
- [ ] Reports scheduled
- [ ] Portfolio case study documented

---

## 💡 Pro Tips

1. **Timing**: GA4 has 1-2 second delay for real-time reports
2. **Case Sensitivity**: Event and parameter names are case-sensitive
3. **24-Hour Wait**: Custom parameters take up to 24 hours to fully process
4. **Preview Mode**: Always test in GTM Preview before going live
5. **Console**: Use browser console to verify data layer before checking GTM
6. **Parameters**: Must match exactly between data layer and GA4 definitions
7. **Timestamps**: Use ISO 8601 format for consistency
8. **Testing**: Test each event individually before running full scenario tests

---

## 📞 Support Resources

- [GTM Setup Guide](https://support.google.com/tagmanager/answer/6103696)
- [GA4 Implementation](https://support.google.com/analytics/answer/9304153)
- [Debug View](https://support.google.com/analytics/answer/7201382)
- [Custom Events](https://support.google.com/analytics/answer/9267744)
- [Conversions](https://support.google.com/analytics/answer/12188663)

---

## ✅ Final Checklist

Before moving to Looker Studio dashboard creation:

- [ ] All 9 events implemented in data layer
- [ ] Data layer validator confirms all events capture correctly
- [ ] GTM Preview shows all tags firing (Green)
- [ ] GA4 Real-time shows all 9 event types
- [ ] All 5 conversions firing and tracking
- [ ] No JavaScript console errors
- [ ] All parameters accurate and present
- [ ] Testing completed on multiple browser sessions
- [ ] 0 critical issues found

**Status**: Ready for next phase? → YES [ ] NO [ ]

---

**Last Updated**: 2025-02-07
**Version**: 1.0
**Status**: Complete & Ready for Testing
