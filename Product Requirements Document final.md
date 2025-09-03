**Product Requirements Document: Samagam Saathi (Phase 1)**

**1.0 Introduction**

This document outlines the product requirements for the initial development phase (Phase 1) of Samagam Saathi, a cross-platform mobile application designed to serve pilgrims at the Mahakumbh 2028.

**1.1 Product Vision**

The vision for Samagam Saathi is to create an indispensable digital companion for Mahakumbh pilgrims that enhances safety, simplifies navigation, and enriches their spiritual journey. The application is designed to function effectively in the unique high-density, low-connectivity environment of the event, empowering users—particularly the most vulnerable—to experience the Mahakumbh with confidence and peace of mind.  

**1.2 Problem Statement**

Pilgrims attending the Mahakumbh face a unique set of significant challenges. These include the risk of separation from family and friends in massive crowds, the difficulty of navigating a complex and temporary event layout, the urgent need to find essential amenities like water or medical aid, and potential language barriers. These problems are critically exacerbated by unreliable mobile connectivity and the diverse demographic of attendees, which ranges from tech-savvy youth to elderly, first-time visitors. Samagam Saathi aims to directly address these issues through an offline-first, user-centric mobile application that remains reliable when it is needed most.  

**1.3 User Personas**

To ensure the application's features are grounded in real-world needs, development will focus on the following user archetypes.

**1.3.1 Primary Persona: Ramesh (The First-Time Elderly Pilgrim)**

Based on the application's core demo narrative, Ramesh is a 65-year-old, first-time pilgrim. His primary needs revolve around safety and accessibility. He requires features like a simple one-tap SOS button, navigation that suggests less crowded routes, an easy way to pin his tent location, and content delivered in his native language (Hindi) via audio guides. Ramesh's journey validates the core value proposition of the application by demonstrating how it provides safety, convenience, and inclusivity.  

**1.3.2 Secondary Persona: The Gupta Family (The Coordinated Group)**

This persona represents a multi-generational family unit, including children and elderly members. Their principal challenge is staying together amidst the crowds. They are the primary users for the "Family & Group Connect" features, relying on real-time location sharing to maintain contact and the ability to pin a common meeting point to regroup if separated.  

**1.3.3 Tertiary Persona: Priya (The Volunteer - Passive Recipient)**

For Phase 1, Priya represents a volunteer or emergency responder who is a _passive_ recipient of system information. While the SOS alert is a mock feature in this initial phase, the system's architecture must be designed with the future in mind, where a real volunteer like Priya would receive an actionable alert. This persona informs the data structure of the SOS payload (e.g., user ID, precise location, timestamp), ensuring it is robust and extensible even in its mock implementation.  

**1.4 Key User Journeys**

The application's success will be measured by its ability to facilitate seamless user journeys that combine multiple features into a cohesive experience. A primary user journey, following the persona of Ramesh, illustrates this integration :  

1.  Upon arrival, Ramesh uses the app to pin the location of his tent on the map, ensuring he can always find his way back.
2.  To visit Triveni Ghat, he uses the Smart Map Navigation to find a route that is both less crowded and passes by essential amenities like a water point.
3.  During his journey, he feels the need for medicine and uses the Amenity Search to find the nearest medical store and navigates to it.
4.  At the Ghat, he taps on the location's icon to listen to a Hindi audio guide explaining its spiritual significance.
5.  Throughout his journey, his live location is shared with his family's group, providing them with peace of mind.
6.  When he feels unwell, he presses the SOS button, which logs an alert that, in a future phase, would be dispatched to a nearby volunteer.

**2.0 Phase 1 Feature Requirements**

This section details the functional requirements for Phase 1, structured as epics containing specific features, user stories, and acceptance criteria. The development strategy for this phase prioritizes validating the core user experience with a polished, reliable MVP using free-tier tools and mock data, thereby de-risking future investment in more complex, real-time data integrations.  

**2.1 Epic: Pilgrim Safety**

**2.1.1 Feature: One-Tap SOS Alert (Mock Implementation)**

*   **User Story:** As a pilgrim feeling unwell or lost, I want to tap a single, prominent SOS button so that my location and an alert can be recorded, making me feel secure.
*   **Acceptance Criteria:**
    1.  **Given** a user is on any primary screen of the app, **When** they see a clearly visible SOS button, **Then** it must be accessible with a single tap.
    2.  **Given** the user taps the SOS button, **When** a confirmation dialog appears to prevent accidental triggers, **And** they confirm the alert, **Then** the app must capture their current GPS coordinates (latitude, longitude) and a timestamp.
    3.  **Given** the alert is confirmed, **When** the device is online, **Then** a structured JSON record containing the user ID, location, and timestamp must be sent to the Supabase Realtime Database.  
    4.  **Given** the alert is confirmed, **Then** the UI must display a confirmation message to the user, stating "Help signal sent. A volunteer will be notified."
*   **Phase 1 Limitation:** This feature does not integrate with any live emergency or volunteer services. The alert is logged to the database for demonstration and data collection purposes only.

**2.1.2 Feature: Safe Zone Indicator (Static Overlay)**

*   **User Story:** As a pilgrim planning my route, I want to see a visual indicator of crowd levels on the map so that I can avoid congested areas and feel safer.
*   **Acceptance Criteria:**
    1.  **Given** a user is viewing the main map, **When** the Safe Zone layer is enabled, **Then** they should see color-coded overlays representing crowd density.
    2.  **Given** the overlays are visible, **Then** they must be rendered with partial transparency so the underlying map details remain visible.
    3.  **Given** the Phase 1 implementation, **Then** these overlays must be based on a pre-defined, static set of geographic polygons (e.g., GeoJSON) categorized as green (safe), yellow (moderate), and red (crowded). This data will be bundled with the app or fetched from Supabase on first load.  
*   **Phase 1 Limitation:** Crowd data is static and does not update in real-time. It serves as a proof-of-concept for future integration with live data sources like CCTV or telecom APIs.

**2.2 Epic: Family & Group Connect**

**2.2.1 Feature: Pin Personal Landmark (Tent/Meeting Point)**

*   **User Story:** As a pilgrim, I want to save the location of my tent or a meeting point on the map with a custom name so that I can easily navigate back to it later.
*   **Acceptance Criteria:**
    1.  **Given** a user is viewing the map, **When** they long-press on a location, **Then** a prompt must appear asking if they want to save this point.
    2.  **Given** the user chooses to save the point, **When** they are prompted to enter a name (e.g., "Our Tent," "Meeting Point Gate 4"), **And** they save it, **Then** a distinct pin icon must appear on the map at the saved coordinates.
    3.  **Given** a pin has been saved, **Then** its data (coordinates, name, user ID) must be persisted in the Supabase/Postgres database and be available offline via local caching (AsyncStorage).  

**2.2.2 Feature: Real-time Group Location Viewing**

*   **User Story:** As a member of a family group, I want to see the live location of my other group members on the map so that we can stay connected and find each other if separated.
*   **Acceptance Criteria:**
    1.  **Given** a user has created or joined a group, **When** they view the map in "Group Mode," **Then** they must see map markers representing the current location of each group member.
    2.  **Given** Group Mode is active and the device is online, **When** a group member's location changes, **Then** their marker on the map must update in near real-time (target latency < 5 seconds).
    3.  **Given** the implementation, **Then** location updates must be handled via the Supabase Realtime Database, with the app using expo-location to fetch and publish the user's own location.  
    4.  **Given** the user taps on a group member's marker, **Then** their name must be displayed.

**2.3 Epic: Smart Map Navigation**

**2.3.1 Feature: Point-to-Point Route Calculation**

*   **User Story:** As a pilgrim, I want to calculate and display the shortest walking route between my current location and a selected destination (like a pinned tent or a POI) so that I can navigate efficiently.
*   **Acceptance Criteria:**
    1.  **Given** a user has selected a destination on the map, **When** they request directions, **Then** the app must calculate and display a polyline on the map representing the shortest path.
    2.  **Given** the Phase 1 implementation, **Then** this calculation will be performed on the client-side using a graph algorithm (e.g., A\*) on a predefined graph of nodes and edges representing the event layout. This client-first approach reduces server load and enhances offline capability.  
    3.  **Given** the route is displayed, **Then** the estimated walking distance and time must also be shown.

**2.3.2 Feature: Alternative Route Calculation (Less Crowded, Amenity-Rich)**

*   **User Story:** As a pilgrim concerned about crowds or needing facilities, I want to choose alternative routes that are either less crowded or pass by more amenities, so that my journey is safer and more convenient.
*   **Acceptance Criteria:**
    1.  **Given** a user is calculating a route, **When** they are presented with routing options, **Then** they must have the choice of "Shortest," "Less Crowded," and "Amenity-Rich."
    2.  **Given** the "Less Crowded" option is selected, **Then** the routing algorithm must apply a higher weight to edges passing through the static "red" and "yellow" crowd zones, favoring a path through "green" zones even if it is longer.  
    3.  **Given** the "Amenity-Rich" option is selected, **Then** the algorithm must prioritize paths that pass within a specified radius (e.g., 50 meters) of amenities like toilets, water points, and medical facilities.  

**2.4 Epic: Personalized Spiritual Journey**

**2.4.1 Feature: Pilgrim Profile Selection**

*   **User Story:** As a new user, I want to select a profile type (e.g., Elderly, Family, Devotee) during onboarding so that the app can provide me with relevant recommendations.
*   **Acceptance Criteria:**
    1.  **Given** a first-time user is completing the initial onboarding flow, **Then** they must be presented with a selection screen for pilgrim type: "Elderly," "Family with Children," "Devotee," "First-timer".  
    2.  **Given** a profile is selected, **Then** this choice must be saved to their user profile in the Supabase database.

**2.4.2 Feature: Static Itinerary Generation**

*   **User Story:** As a pilgrim who has selected a profile, I want to receive a suggested itinerary of places to visit so that I have a structured plan for my spiritual journey.
*   **Acceptance Criteria:**
    1.  **Given** a user with the "Elderly" profile views the "Journey" section, **Then** they must be shown an itinerary that prioritizes less strenuous routes and places with seating.
    2.  **Given** a user with the "Family" profile views the "Journey" section, **Then** the itinerary must include child-friendly locations and highlight nearby amenities.
    3.  **Given** the Phase 1 implementation, **Then** these itineraries are static content (pre-defined lists of POIs, descriptions, and suggested times) stored in the Supabase/Postgres database and associated with a specific pilgrim type.  

**2.5 Epic: Offline Smart Guide**

The offline-first requirement is the central architectural constraint that dictates implementation choices across most features, ensuring the app remains a reliable tool even without an internet connection.  

**2.5.1 Feature: Offline Map and Content Caching**

*   **User Story:** As a pilgrim in an area with no internet, I want to still be able to view the map, my pinned locations, and my itinerary so that the app remains useful at all times.
*   **Acceptance Criteria:**
    1.  **Given** the app is opened for the first time with an internet connection, **When** the initial data download completes, **Then** map tiles for the entire Mahakumbh area, POI data, amenity locations, and itineraries must be cached locally using AsyncStorage or a similar persistent storage solution.  
    2.  **Given** the user is offline, **When** they open the app, **Then** the map, their saved pins, and all static content must be fully accessible.

**2.5.2 Feature: Pre-loaded FAQ Chatbot**

*   **User Story:** As a pilgrim with a common question, I want to ask a simple chatbot and get an instant answer, even when offline, so that I can resolve my query quickly.
*   **Acceptance Criteria:**
    1.  **Given** a user is offline, **When** they open the FAQ Chatbot, **Then** they must be able to type or select from a list of common questions (e.g., "Where is Triveni Ghat?").
    2.  **Given** a pre-loaded question is asked, **Then** the chatbot must provide a pre-scripted answer from its local database.
    3.  **Given** the Phase 1 implementation, **Then** the chatbot's knowledge base is limited to a static set of approximately 50 common Q&As bundled with the app. The functionality will rely on simple keyword-matching or a selection-based system, with no NLP or AI involved.  

**2.5.3 Feature: Text-to-Speech Voice Support**

*   **User Story:** As a pilgrim who has difficulty reading or prefers audio, I want to have the chatbot's answers and POI descriptions read aloud to me in my language so that the app is more accessible.
*   **Acceptance Criteria:**
    1.  **Given** a text answer is displayed by the chatbot or in a POI description, **When** the user taps the "Listen" icon, **Then** the text must be converted to speech and played through the device's speaker.
    2.  **Given** the implementation, **Then** this functionality must be provided by the on-device expo-speech library, ensuring it works fully offline.  
    3.  **Given** the Phase 1 scope, **Then** supported languages for text-to-speech are Hindi and English.

**2.6 Epic: Cultural Immersion**

**2.6.1 Feature: Contextual Audio Guides for Points of Interest**

*   **User Story:** As a pilgrim visiting a significant location, I want to tap on its map icon and listen to a short audio guide about its history and importance so that I can have a more immersive cultural experience.
*   **Acceptance Criteria:**
    1.  **Given** a user is viewing the map, **When** they tap on a designated Point of Interest (POI), **Then** a detail card must appear with a "Play Audio Guide" button.
    2.  **Given** the play button is tapped, **Then** a pre-recorded audio file (MP3) for that POI must be played using the expo-av library.  
    3.  **Given** the offline-first requirement, **Then** these audio files must be pre-generated (using gTTS or similar) and either bundled with the app or downloaded and cached during the initial setup.  
    4.  **Given** the Phase 1 scope, **Then** audio guides will be available in Hindi and English.

**2.7 Epic: Amenity Search & Discovery**

**2.7.1 Feature: Search for Nearest Amenities by Category**

*   **User Story:** As a pilgrim in urgent need of a toilet, I want to quickly search for the nearest one and see it on the map so that I can find it without delay.
*   **Acceptance Criteria:**
    1.  **Given** a user opens the "Amenity Search" feature, **When** they are presented with categories (e.g., "Toilets," "Water," "Medical," "Police"), **Then** they can select one.
    2.  **Given** a category is selected, **Then** the app must calculate and display a list of the 5 nearest amenities of that type, sorted by distance.
    3.  **Given** the implementation, **Then** the distance calculation (e.g., using the Haversine formula) will be performed on the client-side to enhance offline functionality and reduce server load, using the device's current GPS location and the cached amenity dataset.  

**2.7.2 Feature: Display Amenities on Map**

*   **User Story:** As a pilgrim exploring an area, I want to see all nearby amenities on the map so that I am aware of the facilities around me.
*   **Acceptance Criteria:**
    1.  **Given** a user is viewing the map, **When** they enable the "Amenities" layer, **Then** icons representing different amenity types must appear on the map.
    2.  **Given** the user taps on an amenity icon, **Then** its type and name (if available) must be displayed.
    3.  **Given** the offline requirement, **Then** the entire amenity dataset (coordinates and type) must be cached locally for offline use.  

**3.0 Phase 1 Technical Specifications**

This section provides the technical framework for the development team, translating the feature requirements into a concrete implementation plan.

**3.1 System Architecture Overview**

The Phase 1 architecture will follow a client-server model. The client is a React Native (Expo) application designed with an offline-first principle, meaning it primarily operates from a local data cache. The backend is provided by Supabase (BaaS), which handles authentication, database storage, real-time communication, and file storage. An optional, lightweight Node.js service may be used for any custom logic not achievable with Supabase functions, but its use will be minimized. This architecture is designed to be lean and cost-effective for the MVP, while establishing patterns (e.g., structured API payloads) that allow it to scale into a broader event management platform in the future.  

**3.2 Frontend Specifications**

*   **Framework:** React Native with Expo. This is chosen for its cross-platform capabilities (Android/iOS), rapid development cycle, and performance on low-end devices, which are prevalent in the target user base.  
*   **UI Library:** React Native Paper. This library is selected for its clean, accessible Material Design components that are familiar to Android users and align with the app's need for a simple, intuitive interface.  
*   **Mapping Library:** react-native-maps will be used for rendering map tiles, markers, pins, and route polylines.  
*   **State Management:** A lightweight state management library such as Zustand or Redux Toolkit is required to manage global application state, particularly the critical online/offline status and user session data.

**3.3 Backend and Database Specifications**

*   **Primary Backend:** Supabase (Free Tier). The choice of Supabase for the MVP is strategic, leveraging its generous free tier to validate the product without initial infrastructure cost. It will provide :  
    *   **Authentication:** User registration and login, primarily via phone number OTP.
    *   **Database:** A Postgres database for storing all persistent data, including user profiles, pins, amenities, and itineraries.
    *   **Realtime:** The Realtime Database will power the Group Location Sharing feature.
    *   **Storage:** Supabase Storage will be used for hosting static assets like audio guide files.
*   **Custom Logic:** A simple Node.js (Express) server can be provisioned if needed, but the Phase 1 goal is to implement as much logic as possible on the client or within Supabase Functions to maintain a lean backend.

**3.4 Data Models**

The following table outlines the initial database schema in Postgres. A well-defined schema is crucial for ensuring backend and frontend developers have a shared understanding of the data contracts from the project's inception.

| Table Name | Column Name | Data Type | Constraints/Notes |
| --- | --- | --- | --- |
| users | id | uuid | Primary Key, references auth.users.id |
| users | profile_type | text | Enum: 'elderly', 'family', 'devotee', 'first_timer' |
| groups | id | uuid | Primary Key |
| groups | name | text | Name of the family/group |
| group_members | group_id | uuid | Foreign Key to groups.id |
| group_members | user_id | uuid | Foreign Key to users.id |
| pins | id | uuid | Primary Key |
| pins | user_id | uuid | Foreign Key to users.id |
| pins | location | geography(Point, 4326) | Stores latitude/longitude |
| pins | name | text | e.g., "Our Tent" |
| amenities | id | uuid | Primary Key |
| amenities | location | geography(Point, 4326) | Stores latitude/longitude |
| amenities | type | text | Enum: 'toilet', 'water', 'medical', 'police' |

Export to Sheets

**3.5 Offline Caching and Data Synchronization Strategy**

*   **Mechanism:** AsyncStorage will be used for storing structured JSON data (POIs, itineraries, user pins). The device's local file system will be used for larger binary assets like map tiles and audio files.  
*   **Strategy:**
    1.  **Initial Seeding:** On the first launch with an active internet connection, the app will perform a mandatory, one-time download of all data required for offline functionality. The total download size must be optimized to not exceed a reasonable limit (e.g., 100MB).
    2.  **Read Strategy:** The application logic must always attempt to read from the local cache first before checking for network availability.
    3.  **Write Strategy:** When a user creates new data while offline (e.g., saving a pin), the data is written to a local "outbox" queue in AsyncStorage.
    4.  **Synchronization:** Upon restoration of network connectivity, the app will automatically process the outbox queue, sending pending data to the Supabase backend. It will also fetch any updates from the server to refresh its local cache. The UI must clearly indicate the sync status.

**4.0 Non-Functional Requirements (NFRs)**

NFRs define the quality attributes of the system and are critical for user acceptance, especially given the target audience and challenging operating environment.

| Category | Requirement | Metric / Method of Measurement |
| --- | --- | --- |
| Performance | Cold app start time on a low-end device (e.g., 4-year-old Android with 2GB RAM). | Must be < 4 seconds. |
| Performance | Map panning and zooming in offline mode. | Must maintain a fluid frame rate (>30 FPS). |
| Reliability | Application crash rate. | Must be < 0.1% of all user sessions, measured via analytics. |
| Usability | All interactive elements (buttons, icons, links). | Must have a minimum touch target size of 44x44 density-independent pixels (dp). Measured via design review and UI testing. |
| Accessibility | Text contrast ratios for all UI elements. | Must meet Web Content Accessibility Guidelines (WCAG) 2.1 AA standards. Measured using accessibility scanning tools. |
| Offline Functionality | All core features (map viewing, saved pins, itineraries, FAQ chatbot, audio guides). | Must be 100% functional without a network connection. Tested by enabling airplane mode during QA cycles. |
| Storage | Initial offline data cache size. | Must not exceed 100MB to respect storage limitations on low-end devices. |

Export to Sheets

**5.0 Analytics and Success Metrics**

This section defines how the success of Phase 1 will be measured, translating the high-level project goals into trackable metrics.  

**5.1 Key Performance Indicators (KPIs) for Phase 1**

*   **Adoption:**
    *   Number of app downloads.
    *   Daily Active Users (DAU).
*   **Engagement:**
    *   Average number of pins created per user.
    *   Percentage of users who create or join a group.
    *   Total number of routes calculated per day, segmented by type ('shortest', 'less crowded', 'amenity-rich').
    *   Total number of audio guides played.
    *   Number of amenity searches, segmented by category.
*   **Retention:**
    *   Day 1 and Day 7 user retention rates.
*   **Technical Performance:**
    *   Crash-free users percentage (target > 99.9%).

**5.2 Required Analytics Events**

The following specific events must be logged to an analytics platform to track the KPIs.

*   app\_opened, user\_signup, profile\_selected
*   pin\_created, pin\_deleted
*   group\_created, group\_joined
*   route\_calculated (with properties: type: 'shortest' | 'crowded' | 'amenity')
*   amenity\_searched (with property: category: 'toilet' | 'water' | 'medical' | 'police')
*   audio\_guide\_played (with property: poi\_id)
*   sos\_button\_pressed (to track usage of the mock alert feature)

**6.0 Assumptions and Dependencies**

**6.1 Key Assumptions**

*   A static, reliable, and geographically accurate dataset for the Mahakumbh 2028 event area (including paths, points of interest, and amenity locations) will be available prior to the start of development.
*   The target user base will have devices running at least Android 8.0 or iOS 13.
*   Users will grant the necessary permissions for location services, which are essential for the app's core functionality.

**6.2 External Dependencies**

*   **Map Tiles:** The application is dependent on a map tile provider (e.g., OpenStreetMap, Mapbox) whose terms of service and licensing explicitly permit bulk downloading and caching of tiles for offline use. This must be verified during the technical discovery phase.
*   **Supabase:** The project relies on the Supabase free tier for Phase 1. Development and testing must operate within the documented limitations on database size, API requests, and concurrent real-time connections.  

**7.0 Scope Delimitation: Future Considerations**

To manage stakeholder expectations and prevent scope creep, this section explicitly defines what is _not_ being built in Phase 1. This table serves as both a boundary for the current project and a high-level roadmap for future phases.

| Feature Area | In Scope for Phase 1 | Out of Scope (Reserved for Future Phases) |
| --- | --- | --- |
| SOS Alert | Mock alert logged to the application's database with a UI confirmation message for the user. | Integration with live volunteer, police, or emergency dispatch systems for real-time response. |
| Crowd Data | Static, pre-defined heatmap overlays (green/yellow/red zones) bundled with the app. | Real-time crowd density data sourced from telecom APIs, CCTV feeds, or IoT sensors. |
| Navigation | Routing on a pre-defined graph of paths exclusively within the Mahakumbh event area. | Integration with global GIS APIs (e.g., Google Maps) for routing outside the event; real-time traffic/congestion updates. |
| FAQ Chatbot | Simple keyword matching on a small, static, pre-loaded set of questions and answers. | AI/NLP-powered chatbot using services like Hugging Face for natural language understanding and dynamic, multilingual support. |
| Backend Scaling | Hosted Supabase free tier with a lightweight, optional Node.js service. | Self-hosted Postgres cluster with replication, Redis caching, and horizontally scaled microservices on a cloud provider (AWS/GCP) using Docker and Kubernetes. |
| User Authentication | Simple phone number OTP login. | Social logins (Google, Facebook), biometric authentication (fingerprint/face ID). |
| Content | Static itineraries and audio guides in Hindi and English. | Dynamic, user-generated content (reviews, tips), support for additional regional languages, and video guides. |