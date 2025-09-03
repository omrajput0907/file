# Samagam Saathi App Flow Document
*Version 1.0 - Phase 1 Implementation*

## 1. Executive Summary

This app flow document translates the Samagam Saathi PRD into detailed user interaction flows, screen sequences, and navigation patterns. It serves as a blueprint for designers and developers to understand the complete user journey from onboarding to core feature usage.

## 2. App Architecture & Navigation Structure

### 2.1 Primary Navigation Pattern
- **Tab-based Navigation** (Bottom Navigation Bar)
  - Home/Map (Primary)
  - Journey (Itineraries)
  - Groups (Family Connect)
  - Help (FAQ Chatbot)
  - Profile

### 2.2 Information Architecture
```
Samagam Saathi App
├── Onboarding Flow
├── Main Application
│   ├── Home/Map Tab
│   │   ├── Map View (Default)
│   │   ├── Amenity Search
│   │   ├── Route Planning
│   │   └── Emergency SOS
│   ├── Journey Tab
│   │   ├── Recommended Itineraries
│   │   ├── Audio Guides
│   │   └── POI Details
│   ├── Groups Tab
│   │   ├── Create/Join Group
│   │   ├── Group Map View
│   │   └── Group Management
│   ├── Help Tab
│   │   ├── FAQ Chatbot
│   │   ├── Voice Support
│   │   └── Language Settings
│   └── Profile Tab
│       ├── Personal Info
│       ├── Saved Pins
│       ├── Profile Type
│       └── Settings
└── Emergency Flows
```

## 3. Detailed User Flows

### 3.1 First-Time User Onboarding Flow

**Entry Point:** App Launch (First Time)

**Flow Sequence:**
1. **Splash Screen** (2-3 seconds)
   - App logo and loading indicator
   - Background: Mahakumbh imagery

2. **Welcome Screen**
   - Brief app description
   - Language selection (Hindi/English)
   - CTA: "Get Started"

3. **Permissions Request**
   - Location Permission (Critical)
   - Storage Permission
   - Clear explanation of why each is needed
   - Options: "Allow" / "Learn More" / "Skip for now"

4. **Profile Setup**
   - **Screen Title:** "Tell us about yourself"
   - **Profile Options:**
     - Elderly Pilgrim
     - Family with Children
     - Devotee
     - First-timer
   - **Each option shows:**
     - Icon representation
     - Brief description
     - Benefits specific to that profile

5. **Phone Number Verification**
   - Enter phone number
   - OTP verification
   - Account creation in Supabase

6. **Initial Data Download**
   - Progress indicator
   - Download size estimate
   - Offline content preparation
   - Success confirmation

7. **Quick Tutorial** (Optional, skippable)
   - 3-4 key feature highlights
   - Interactive elements
   - "Skip" option available

8. **Welcome to Main App**
   - Direct to Home/Map tab

### 3.2 Core Map & Navigation Flow

**Entry Point:** Home/Map Tab (Default landing screen)

**Primary Screen Elements:**
- Full-screen map view
- Floating SOS button (bottom-right, prominent red)
- Search bar (top)
- Layer toggle buttons (top-right)
- Bottom navigation tabs
- User location indicator

**User Interactions & Sub-flows:**

#### 3.2.1 Pin Creation Flow
**Trigger:** Long press on map location
1. **Context Menu Appears**
   - "Save this location"
   - "Get directions here"
   - "Cancel"

2. **Pin Creation Dialog** (if "Save this location" selected)
   - Text input: "Name this location"
   - Placeholder examples: "Our Tent", "Meeting Point"
   - Buttons: "Save" / "Cancel"

3. **Confirmation**
   - Pin appears on map with custom icon
   - Toast message: "Location saved successfully"
   - Pin stored locally and synced when online

#### 3.2.2 Route Planning Flow
**Trigger:** Tap on any destination (POI, pin, amenity)
1. **Destination Info Card** (Bottom sheet)
   - Location name/type
   - Distance from current location
   - "Get Directions" button
   - "Play Audio Guide" button (if POI)

2. **Route Options Screen**
   - **Route Types:**
     - Shortest (default)
     - Less Crowded
     - Amenity-Rich
   - Distance and time estimates for each
   - "Start Navigation" button

3. **Active Navigation View**
   - Route polyline on map
   - Turn-by-turn directions (text)
   - Distance remaining
   - "End Navigation" button

#### 3.2.3 Safe Zone Visualization Flow
**Trigger:** Toggle "Safe Zones" layer
1. **Layer Activation**
   - Color-coded overlays appear on map
   - Legend appears (Green: Safe, Yellow: Moderate, Red: Crowded)
   - Toggle to turn off

### 3.3 Emergency SOS Flow

**Entry Point:** SOS Button (Prominent red floating button)

**Flow Sequence:**
1. **First Tap**
   - Button animation/feedback
   - Confirmation dialog appears

2. **Confirmation Dialog**
   - **Title:** "Emergency Alert"
   - **Message:** "Are you sure you want to send an emergency signal?"
   - **Buttons:** 
     - "Yes, Send Alert" (Primary, red)
     - "Cancel" (Secondary)

3. **Alert Processing** (if confirmed)
   - GPS location capture
   - Timestamp generation
   - Data package creation (User ID + Location + Timestamp)
   - Attempt to send to Supabase (if online)
   - Store in local queue (if offline)

4. **User Feedback**
   - Success screen with checkmark
   - Message: "Help signal sent. A volunteer will be notified."
   - "OK" button to dismiss
   - Return to previous screen

### 3.4 Family & Group Connect Flow

**Entry Point:** Groups Tab

#### 3.4.1 Group Creation Flow
1. **Groups Landing Screen**
   - "Create New Group" button
   - "Join Existing Group" button
   - List of current groups (if any)

2. **Create Group Screen**
   - Group name input
   - Group description (optional)
   - "Create Group" button

3. **Group Created Success**
   - Group code displayed
   - "Share Group Code" button
   - "Go to Group Map" button

#### 3.4.2 Group Joining Flow
1. **Join Group Screen**
   - Group code input field
   - "Join Group" button

2. **Group Validation**
   - Code verification
   - Group details preview
   - "Confirm Join" button

3. **Group Map View**
   - Map with all group member locations
   - Different colored pins for each member
   - Real-time location updates
   - Member list sidebar

### 3.5 Amenity Search Flow

**Entry Point:** Search bar or dedicated amenity button

**Flow Sequence:**
1. **Search Interface**
   - **Search Methods:**
     - Category buttons (Toilets, Water, Medical, Police)
     - Text search bar
     - "Near Me" quick action

2. **Category Selection**
   - Visual category grid
   - Icons and labels
   - Tap to select category

3. **Results Display**
   - **List View:**
     - 5 nearest amenities
     - Name, type, distance
     - "View on Map" / "Get Directions" for each
   - **Map View:**
     - Amenity pins overlaid on map
     - Different icons per amenity type

4. **Amenity Details**
   - Basic information
   - Operating hours (if available)
   - "Get Directions" CTA

### 3.6 Spiritual Journey & Audio Guides Flow

**Entry Point:** Journey Tab or POI tap on map

#### 3.6.1 Itinerary Browsing Flow
1. **Journey Landing Screen**
   - Profile-based itinerary recommendations
   - "Today's Suggestions" section
   - "All Sacred Places" section
   - Search functionality

2. **Itinerary Detail View**
   - List of recommended POIs
   - Estimated time and distance
   - "Start This Journey" button

#### 3.6.2 Audio Guide Flow
**Trigger:** Tap POI on map or in itinerary
1. **POI Information Card**
   - Name and brief description
   - "Play Audio Guide" button with speaker icon
   - Available languages indicator

2. **Audio Player Interface**
   - Play/pause controls
   - Progress bar
   - Language switcher (Hindi/English)
   - "Listen" icon for text-to-speech of written content

### 3.7 FAQ Chatbot Flow

**Entry Point:** Help Tab

**Flow Sequence:**
1. **Chatbot Landing Screen**
   - Welcome message
   - Quick question suggestions (buttons)
   - Text input for custom questions
   - Voice input option

2. **Interaction Patterns**
   - **Quick Questions:** Tap pre-defined question → Immediate answer
   - **Text Input:** Type question → Keyword matching → Response
   - **Follow-up:** Related question suggestions after each answer

3. **Response Interface**
   - Text answer display
   - "Listen" button for text-to-speech
   - "Was this helpful?" feedback
   - Related questions suggestions

## 4. Screen Wireflow Descriptions

### 4.1 Critical Screen Transitions

#### Home/Map Tab Flow
```
App Launch → Onboarding (first time) → Map View
                    ↓
Map View ← → [POI Details] ← → [Audio Guide Player]
    ↓
[Route Planning] ← → [Navigation View]
    ↓
[Amenity Search] ← → [Amenity Results] ← → [Amenity Details]
```

#### Emergency Flow
```
Any Screen → SOS Button Tap → Confirmation Dialog → Alert Sent → Success Message → Return to Previous Screen
```

#### Group Management Flow
```
Groups Tab → Create/Join Group → Group Setup → Group Map View → Real-time Tracking
```

### 4.2 State Management Considerations

**Global App States:**
- Online/Offline status
- Current user location
- Active group membership
- Current navigation route
- Emergency alert status

**Screen-Level States:**
- Map layer toggles (amenities, safe zones, group members)
- Audio playback status
- Search query and results
- Form inputs and validation

## 5. Error Handling & Edge Case Flows

### 5.1 Connectivity Issues
**Scenario:** User loses internet connection
- **Flow:** Graceful degradation to offline mode
- **UI Indicators:** Offline banner, sync status indicators
- **Functionality:** All core features remain available

### 5.2 Location Services Disabled
**Scenario:** User denies location permission
- **Flow:** Permission re-request with explanation
- **Fallback:** Manual location selection on map
- **Feature Impact:** Route planning limited, group sharing disabled

### 5.3 Emergency Scenarios
**Scenario:** SOS activated while offline
- **Flow:** Alert queued locally → Sync when connectivity restored
- **User Feedback:** "Alert queued, will send when connection available"

## 6. Accessibility & Usability Considerations

### 6.1 Touch Targets
- Minimum 44dp for all interactive elements
- Extra padding around critical buttons (SOS)
- Swipe gestures for map navigation

### 6.2 Visual Accessibility
- High contrast mode support
- Text size scaling
- Clear visual hierarchy
- Color-blind friendly palette for safe zone indicators

### 6.3 Language & Audio Support
- Hindi/English interface switching
- Text-to-speech for all critical content
- Audio cues for navigation guidance

## 7. Technical Flow Considerations

### 7.1 Data Synchronization Flow
```
App Launch → Check Connectivity → Load from Cache → Display UI
                    ↓
Background: Sync Queue Processing → Update Cache → Update UI
```

### 7.2 Real-time Features Flow
```
Group Location Sharing:
User Location Update → Local State Update → Supabase Realtime → Other Group Members → Map Update
```

## 8. Success Metrics Integration

### 8.1 Analytics Event Triggers
- Screen views automatically tracked
- User interactions logged at decision points
- Feature usage metrics captured
- Performance metrics (load times, errors) monitored

### 8.2 User Journey Funnels
- Onboarding completion rate
- Feature adoption rates
- User retention at key interaction points

## 9. Implementation Prioritization

### 9.1 MVP Critical Path
1. **Core Navigation:** Map view, basic routing
2. **Safety Features:** Pin saving, SOS mock implementation
3. **Offline Functionality:** Data caching, offline map access
4. **Basic Group Features:** Location sharing

### 9.2 Enhancement Features
1. **Audio Guides:** POI information and cultural content
2. **Advanced Routing:** Crowd-aware and amenity-rich routing
3. **Enhanced Search:** Category-based amenity discovery

This app flow document provides the foundation for UI/UX design, development sprint planning, and QA testing scenarios. Each flow should be validated through user testing with representatives from the target personas, particularly focusing on the elderly pilgrim use case to ensure accessibility and ease of use.