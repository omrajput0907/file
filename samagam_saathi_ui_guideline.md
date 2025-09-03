# Samagam Saathi - Frontend UI/UX Guidelines
*Version 1.0 - Comprehensive Design System & Implementation Guide*

## 1. Design Philosophy & Principles

### 1.1 Core Design Values
- **Inclusivity First**: Design for 65-year-old Ramesh, and everyone else will benefit
- **Offline-First Resilience**: Every UI element must work without connectivity
- **Cultural Sensitivity**: Respect religious sentiments while maintaining modern usability
- **Crisis-Ready Design**: Clear, calm, and actionable in emergency situations
- **Progressive Disclosure**: Simple at first glance, powerful when needed

### 1.2 Design Principles

#### Principle 1: Clarity Over Cleverness
- Use familiar patterns that elderly users recognize
- Avoid trendy interactions that might confuse
- Text should be readable at arm's length
- Icons must be universally understood or labeled

#### Principle 2: Trust Through Consistency
- Same actions produce same results everywhere
- Visual language remains uniform across all screens
- Predictable navigation patterns
- Consistent feedback mechanisms

#### Principle 3: Forgiveness in Design
- All actions are reversible or confirmable
- Clear undo options for critical actions
- Graceful error recovery
- Multiple paths to accomplish tasks

#### Principle 4: Contextual Intelligence
- Show relevant information based on time and location
- Adapt UI density based on user profile
- Smart defaults that learn from usage
- Proactive assistance without being intrusive

## 2. Visual Design System

### 2.1 Color Palette

#### Primary Colors
```css
/* Brand Colors */
--primary-saffron: #FF9933;      /* Sacred, energetic - main CTA */
--primary-blue: #138808;         /* Trust, reliability - navigation */
--primary-white: #FFFFFF;        /* Purity, space - backgrounds */

/* Semantic Colors */
--success-green: #4CAF50;        /* Completed actions, safe zones */
--warning-yellow: #FFC107;       /* Moderate crowds, caution */
--danger-red: #F44336;           /* Emergency, crowded areas */
--info-blue: #2196F3;            /* Information, tips */

/* Neutral Palette */
--gray-900: #212121;             /* Primary text */
--gray-700: #616161;             /* Secondary text */
--gray-500: #9E9E9E;             /* Disabled states */
--gray-300: #E0E0E0;             /* Borders */
--gray-100: #F5F5F5;             /* Backgrounds */

/* Accessibility Colors */
--high-contrast-black: #000000;  /* High contrast mode */
--high-contrast-yellow: #FFFF00; /* Focus indicators */
```

#### Color Usage Guidelines
- **60-30-10 Rule**: 60% neutral (white/gray), 30% primary (saffron), 10% accent
- **Contrast Ratios**: Minimum 4.5:1 for normal text, 3:1 for large text
- **Cultural Context**: Saffron for spiritual elements, green for safety
- **State Colors**: Consistent semantic meaning across all features

### 2.2 Typography

#### Font Stack
```css
/* Primary Font Family */
font-family: 'Roboto', 'Noto Sans Devanagari', -apple-system, BlinkMacSystemFont, sans-serif;

/* Display Font (for headers) */
font-family: 'Poppins', 'Roboto', sans-serif;

/* Monospace (for codes/numbers) */
font-family: 'Roboto Mono', 'Courier New', monospace;
```

#### Type Scale
```css
/* Mobile-First Scale (base: 16px) */
--text-xs: 0.75rem;     /* 12px - Captions, labels */
--text-sm: 0.875rem;    /* 14px - Secondary text */
--text-base: 1rem;      /* 16px - Body text */
--text-lg: 1.125rem;    /* 18px - Emphasized body */
--text-xl: 1.25rem;     /* 20px - Section headers */
--text-2xl: 1.5rem;     /* 24px - Page titles */
--text-3xl: 1.875rem;   /* 30px - Main headers */

/* Line Heights */
--leading-tight: 1.25;
--leading-normal: 1.5;
--leading-relaxed: 1.75;

/* Font Weights */
--font-normal: 400;
--font-medium: 500;
--font-semibold: 600;
--font-bold: 700;
```

#### Typography Rules
- **Minimum font size**: 14px for any interactive text
- **Body text**: 16px minimum, 18px preferred for elderly users
- **Line length**: 45-75 characters for optimal readability
- **Hindi text**: Increase size by 10% for Devanagari script

### 2.3 Spacing System

```css
/* Base Unit: 4px */
--space-1: 0.25rem;   /* 4px */
--space-2: 0.5rem;    /* 8px */
--space-3: 0.75rem;   /* 12px */
--space-4: 1rem;      /* 16px */
--space-5: 1.25rem;   /* 20px */
--space-6: 1.5rem;    /* 24px */
--space-8: 2rem;      /* 32px */
--space-10: 2.5rem;   /* 40px */
--space-12: 3rem;     /* 48px */
--space-16: 4rem;     /* 64px */
```

### 2.4 Elevation & Shadows

```css
/* Shadow Levels */
--shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
--shadow-md: 0 4px 6px rgba(0,0,0,0.1);
--shadow-lg: 0 10px 15px rgba(0,0,0,0.1);
--shadow-xl: 0 20px 25px rgba(0,0,0,0.1);

/* Emergency Shadow */
--shadow-emergency: 0 0 20px rgba(244,67,54,0.5);
```

### 2.5 Border Radius

```css
--radius-sm: 0.25rem;   /* 4px - Buttons, inputs */
--radius-md: 0.5rem;    /* 8px - Cards */
--radius-lg: 1rem;      /* 16px - Modals */
--radius-full: 9999px;  /* Pills, circular buttons */
```

## 3. Component Library Specifications

### 3.1 Buttons

#### Primary Button (CTA)
```jsx
/* Specifications */
- Height: 48px minimum (56px for critical actions)
- Padding: 16px horizontal minimum
- Font: 16px semibold
- Color: White text on saffron background
- Border radius: 8px
- Touch target: 48x48px minimum
- States: Default, Pressed, Disabled, Loading

/* Example */
<Button variant="primary" size="large">
  Get Directions
</Button>
```

#### Emergency SOS Button
```jsx
/* Specifications */
- Size: 64x64px (always visible)
- Position: Bottom-right, 16px from edges
- Color: Danger red (#F44336)
- Icon: 24px white SOS/emergency icon
- Animation: Subtle pulse every 3 seconds
- Shadow: Extra elevation for prominence
- Haptic feedback on press

/* Interaction */
- Single tap: Shows confirmation
- Long press (3s): Direct emergency trigger
```

#### Button Hierarchy
1. **Primary**: Main actions (saffron)
2. **Secondary**: Alternative actions (outlined)
3. **Tertiary**: Less important (text only)
4. **Danger**: Destructive/emergency (red)
5. **Ghost**: Subtle actions (transparent)

### 3.2 Navigation Components

#### Bottom Navigation Bar
```jsx
/* Specifications */
- Height: 56px (Android) / 83px (iOS with safe area)
- Items: 5 maximum
- Icon size: 24x24px
- Label: 12px font, always visible
- Active indicator: Saffron color + background pill
- Badge support for notifications

/* Structure */
<BottomNav>
  <NavItem icon="map" label="Map" active />
  <NavItem icon="journey" label="Journey" />
  <NavItem icon="group" label="Groups" />
  <NavItem icon="help" label="Help" />
  <NavItem icon="profile" label="Profile" />
</BottomNav>
```

#### Header/App Bar
```jsx
/* Specifications */
- Height: 56px
- Background: White with subtle shadow
- Title: 20px semibold, centered or left-aligned
- Actions: Maximum 2 icon buttons on right
- Back button: 24px arrow icon on left
```

### 3.3 Cards & Containers

#### Information Card
```jsx
/* Specifications */
- Padding: 16px
- Border radius: 12px
- Background: White
- Shadow: shadow-md
- Border: 1px solid gray-200 (optional)

/* Content Structure */
<Card>
  <CardHeader>
    <Icon /> <Title />
  </CardHeader>
  <CardBody>
    Content with proper spacing
  </CardBody>
  <CardActions>
    <Button>Action</Button>
  </CardActions>
</Card>
```

#### Bottom Sheet
```jsx
/* Specifications */
- Border radius: 16px top corners only
- Drag handle: 4x32px gray bar
- Max height: 90% of screen
- Swipe to dismiss gesture
- Background overlay: 50% black
```

### 3.4 Forms & Inputs

#### Text Input
```jsx
/* Specifications */
- Height: 48px minimum
- Font size: 16px (prevents zoom on iOS)
- Border: 1px solid gray-300
- Focus: 2px saffron border
- Error: Red border with helper text
- Label: Always visible (floating or top)
- Helper text: 14px below input

/* Accessibility */
- Clear label association
- Error messages announced
- Sufficient color contrast
```

#### OTP Input
```jsx
/* Specifications */
- 6 boxes, 40x48px each
- 8px spacing between boxes
- Auto-focus next box
- Large numeric keyboard
- Clear visual feedback
```

### 3.5 Map Components

#### Map Markers/Pins
```jsx
/* Types & Sizes */
- User location: 16px blue dot with pulse
- Saved pin: 32px custom icon
- Group member: 24px colored circle with initial
- Amenity: 24px category icon
- POI: 32px place icon

/* Interaction */
- Tap: Shows info card
- Long press: Shows options menu
```

#### Route Polyline
```jsx
/* Specifications */
- Width: 4px for selected route
- Color: Primary blue with white outline
- Alternative routes: Gray, 2px width
- Animated direction arrows
```

#### Crowd Density Overlay
```css
/* Specifications */
- Green zones: rgba(76, 175, 80, 0.3)
- Yellow zones: rgba(255, 193, 7, 0.3)
- Red zones: rgba(244, 67, 54, 0.3)
- Smooth gradient transitions
- 50% opacity for map visibility
```

### 3.6 Feedback & Status

#### Toast Messages
```jsx
/* Specifications */
- Position: Bottom, above navigation
- Duration: 3 seconds (standard), 5 seconds (important)
- Max width: 90% of screen
- Actions: Optional single action button
- Swipe to dismiss: Supported
```

#### Loading States
```jsx
/* Types */
1. Skeleton screens for content
2. Circular progress for actions
3. Linear progress for downloads
4. Shimmer effect for cards

/* Offline Indicator */
- Persistent banner below header
- Yellow background with icon
- "Offline Mode" text
```

## 4. Interaction Patterns

### 4.1 Gesture Support

#### Supported Gestures
- **Tap**: Primary selection
- **Double tap**: Zoom in on map
- **Long press**: Context menu
- **Pinch**: Zoom map
- **Swipe**: Navigate between screens
- **Pull to refresh**: Update content (when online)

#### Gesture Feedback
- **Haptic**: Light feedback for actions
- **Visual**: Ripple effect on touch
- **Audio**: Optional sound feedback

### 4.2 Animation Guidelines

#### Animation Principles
- **Duration**: 200-300ms for most transitions
- **Easing**: ease-in-out for natural feel
- **Purpose**: Guide attention, show relationships
- **Performance**: 60fps minimum, CSS transforms preferred

#### Standard Animations
```css
/* Transition Timing */
--transition-fast: 150ms;
--transition-base: 250ms;
--transition-slow: 350ms;

/* Easing Functions */
--ease-in-out: cubic-bezier(0.4, 0, 0.2, 1);
--ease-out: cubic-bezier(0, 0, 0.2, 1);
--ease-in: cubic-bezier(0.4, 0, 1, 1);
```

### 4.3 Microinteractions

#### Button Press
- Scale down to 0.95
- Darken background by 10%
- Duration: 100ms

#### Card Selection
- Elevate with shadow
- Subtle scale to 1.02
- Border highlight

#### Success Feedback
- Checkmark animation
- Green pulse effect
- Haptic success pattern

## 5. Accessibility Guidelines

### 5.1 Visual Accessibility

#### Requirements
- **WCAG 2.1 AA Compliance**
- **Contrast Ratios**: 4.5:1 minimum
- **Focus Indicators**: 2px minimum outline
- **Color Independence**: Never rely solely on color
- **Text Scaling**: Support up to 200% zoom

#### Implementation
```css
/* Focus Styles */
:focus-visible {
  outline: 2px solid var(--primary-saffron);
  outline-offset: 2px;
}

/* High Contrast Mode */
@media (prefers-contrast: high) {
  /* Increased contrast styles */
}
```

### 5.2 Motor Accessibility

#### Touch Targets
- **Minimum Size**: 48x48dp
- **Spacing**: 8dp between targets
- **Edge Targets**: 16dp from screen edge
- **Grouped Actions**: Logical clustering

### 5.3 Cognitive Accessibility

#### Guidelines
- **Clear Labels**: Descriptive, not clever
- **Consistent Patterns**: Same actions everywhere
- **Error Prevention**: Confirmation for critical actions
- **Help Available**: Context-sensitive help
- **Simple Language**: Grade 6 reading level

### 5.4 Screen Reader Support

#### Implementation Requirements
- **Semantic HTML**: Proper heading hierarchy
- **ARIA Labels**: For icon-only buttons
- **Live Regions**: For dynamic updates
- **Focus Management**: Logical tab order

```jsx
/* Example */
<button 
  aria-label="Send emergency alert"
  aria-describedby="sos-help-text"
>
  <SOSIcon />
</button>
```

## 6. Responsive Design

### 6.1 Breakpoints

```css
/* Mobile-First Breakpoints */
--screen-sm: 360px;   /* Small phones */
--screen-md: 390px;   /* Standard phones */
--screen-lg: 428px;   /* Large phones */
--screen-xl: 768px;   /* Tablets */
```

### 6.2 Adaptive Layouts

#### Phone Portrait (Primary)
- Single column layouts
- Full-width components
- Vertical scrolling
- Bottom navigation

#### Phone Landscape
- Two-column where beneficial
- Reduced vertical spacing
- Side navigation option
- Horizontal scrolling for lists

#### Tablet
- Multi-column layouts
- Increased information density
- Split-view support
- Expanded navigation

### 6.3 Safe Areas

```css
/* iOS Safe Areas */
padding-top: env(safe-area-inset-top);
padding-bottom: env(safe-area-inset-bottom);
padding-left: env(safe-area-inset-left);
padding-right: env(safe-area-inset-right);
```

## 7. Platform-Specific Guidelines

### 7.1 Android Adaptations

#### Material Design Alignment
- Floating Action Button for SOS
- Material ripple effects
- Bottom sheets follow Material specs
- System back button support

#### Android-Specific Features
- Hardware back button handling
- Android toast style messages
- Material date/time pickers
- Native share sheet integration

### 7.2 iOS Adaptations

#### iOS Design Patterns
- iOS-style navigation bars
- Swipe-back gesture support
- iOS modal presentations
- SF Symbols where appropriate

#### iOS-Specific Features
- Haptic feedback patterns
- iOS action sheets
- Native iOS alerts
- Dynamic Type support

## 8. Performance Guidelines

### 8.1 Rendering Performance

#### Requirements
- **First Paint**: < 1 second
- **Interactive**: < 3 seconds
- **Smooth Scrolling**: 60fps
- **Animation**: 60fps minimum

#### Optimization Techniques
```jsx
/* List Virtualization */
<FlatList
  data={items}
  renderItem={renderItem}
  getItemLayout={getItemLayout}
  removeClippedSubviews={true}
  maxToRenderPerBatch={10}
  windowSize={10}
/>

/* Image Optimization */
- Use WebP format where supported
- Lazy load images outside viewport
- Progressive loading for large images
- Cached thumbnails for lists
```

### 8.2 Memory Management

#### Guidelines
- **Image Caching**: Maximum 50MB
- **Map Tiles**: Aggressive cleanup
- **State Management**: Clear unused data
- **List Items**: Recycle views

### 8.3 Battery Optimization

#### Power-Saving Measures
- Reduce GPS polling when stationary
- Batch network requests
- Minimize background processing
- Dark mode support for OLED screens

## 9. Localization & Internationalization

### 9.1 Language Support

#### Primary Languages
- **Hindi**: Primary language, RTL support
- **English**: Secondary language

#### Text Guidelines
```jsx
/* Specifications */
- Hindi text: 110% of English size
- Devanagari line height: 1.6x
- Allow 30% extra space for Hindi
- Number formatting: Indian system (lakhs, crores)

/* Implementation */
const strings = {
  en: {
    welcome: "Welcome to Mahakumbh",
    sos: "Emergency"
  },
  hi: {
    welcome: "महाकुंभ में आपका स्वागत है",
    sos: "आपातकाल"
  }
};
```

### 9.2 Cultural Considerations

#### Visual Elements
- Respectful imagery for religious content
- Traditional color symbolism
- Appropriate iconography
- Cultural gesture considerations

#### Content Presentation
- Right-to-left support for future Urdu
- Date format: DD/MM/YYYY
- Time format: 12-hour with AM/PM
- Temperature: Celsius

## 10. Dark Mode Considerations

### 10.1 Color Adaptations

```css
/* Dark Mode Palette */
@media (prefers-color-scheme: dark) {
  --bg-primary: #121212;
  --bg-secondary: #1E1E1E;
  --text-primary: #FFFFFF;
  --text-secondary: #B0B0B0;
  
  /* Maintain semantic colors */
  --danger-red: #FF5252;
  --success-green: #69F0AE;
}
```

### 10.2 Implementation Strategy

- System preference detection
- Manual toggle in settings
- Preserve semantic meaning
- Reduce bright colors intensity
- Increase contrast for readability

## 11. Testing & Validation

### 11.1 Device Testing Matrix

#### Priority Devices
1. **Low-end Android**: 2GB RAM, Android 8+
2. **Mid-range Android**: 4GB RAM, Android 10+
3. **iPhone SE**: Smallest iOS screen
4. **iPhone 13**: Standard iOS
5. **iPad**: Tablet layout testing

### 11.2 Accessibility Testing

#### Tools & Methods
- Screen reader testing (TalkBack, VoiceOver)
- Keyboard navigation testing
- Color contrast analyzers
- One-handed operation testing
- Elder user testing sessions

### 11.3 Performance Testing

#### Metrics to Monitor
- Time to interactive
- Frame rate during animations
- Memory usage over time
- Battery consumption
- Offline functionality

## 12. Component States Documentation

### 12.1 Interactive States

Every interactive component must handle:
- **Default**: Resting state
- **Hover**: Desktop only
- **Focus**: Keyboard navigation
- **Active**: Being pressed
- **Disabled**: Non-interactive
- **Loading**: Processing
- **Error**: Invalid state
- **Success**: Completed state

### 12.2 Data States

#### Content Loading States
1. **Empty**: No data available
2. **Loading**: Fetching data
3. **Error**: Failed to load
4. **Success**: Data loaded
5. **Offline**: Cached data shown

## 13. Emergency UI Patterns

### 13.1 Crisis Mode Design

#### When Activated
- Simplified interface
- Larger touch targets
- High contrast colors
- Essential functions only
- Clear exit path

#### SOS Interface
- Full-screen takeover
- Countdown timer
- Cancel option prominent
- Location display
- Status feedback

### 13.2 Panic Prevention

- Calm color choices in emergency
- Clear, simple instructions
- Progressive disclosure of options
- Reassuring messaging
- Visual breathing guides

## 14. Implementation Checklist

### 14.1 Pre-Development
- [ ] Design tokens defined
- [ ] Component library setup
- [ ] Accessibility audit plan
- [ ] Device testing matrix
- [ ] Performance budgets set

### 14.2 During Development
- [ ] Component documentation
- [ ] Accessibility annotations
- [ ] Performance monitoring
- [ ] Cross-platform testing
- [ ] Localization testing

### 14.3 Pre-Launch
- [ ] Elder user testing
- [ ] Offline mode validation
- [ ] Emergency flow testing
- [ ] Load testing
- [ ] Accessibility certification

## 15. Design Handoff Specifications

### 15.1 Asset Delivery

#### Image Assets
- **Format**: PNG for icons, WebP for photos
- **Sizes**: 1x, 2x, 3x for all assets
- **Naming**: component_state_size (e.g., btn_sos_pressed_2x)

#### Icon Library
- 24x24dp base size
- Outline style for inactive
- Filled style for active
- SVG format preferred

### 15.2 Documentation Requirements

Each component needs:
1. Visual specifications
2. Interaction documentation
3. State definitions
4. Accessibility notes
5. Platform variations
6. Code examples

## Appendix A: Quick Reference

### Critical Measurements
- Touch target: 48x48dp minimum
- Text: 16px minimum
- SOS button: 64x64dp
- Bottom nav: 56dp height
- Card padding: 16dp
- Screen margins: 16dp

### Critical Colors
- Emergency: #F44336
- Safe: #4CAF50
- Warning: #FFC107
- Primary CTA: #FF9933

### Critical Animations
- Standard transition: 250ms
- Loading timeout: 30 seconds
- Toast duration: 3 seconds
- Emergency countdown: 5 seconds

---

*This guideline is a living document and should be updated based on user testing feedback and technical constraints discovered during development.*