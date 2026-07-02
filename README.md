# 🗺️ Travelobe — AI Travel Planner & Social Platform

Travelobe is a production-ready, full-stack, AI-powered travel planning companion and real-time social platform. By integrating the **Google Gemini AI API**, **Google Places API**, **Firebase**, and **Spring Boot Microservices**, Travelobe allows users to generate highly customized, day-by-day travel itineraries in seconds, complete with hotel recommendations, activity schedules, and estimated travel times.

It also features a secure Google Sign-In interface, a MySQL-backed review and feedback dashboard, and a real-time messaging system powered by WebSockets (STOMP/SockJS).

---

## 🚀 Key Features

*   **🧠 AI-Driven Itinerary Generation:** Leverages `gemini-1.5-flash` to construct rich, structured, JSON-formatted travel plans based on target destinations, duration (up to 5 days), budget tiers (Cheap, Moderate, Luxury), and travel companions (Solo, Couple, Family, Friends).
*   **📍 Google Places Integration:** Uses Google Places Autocomplete (v1 API) for smart destination searches and dynamic place/hotel photos retrieval.
*   **🔐 Secure Google OAuth Authentication:** Simple, secure profile authentication utilizing `@react-oauth/google`.
*   **☁️ Cloud-Backed Trip Storage:** Uses Firebase Firestore to save generated itineraries, making them easily retrievable under unique URLs for shareability.
*   **💬 Real-Time Chat Club:** Powered by Spring Boot WebSocket and STOMP messaging protocol to allow travelers to connect, chat, and share recommendations instantly.
*   **✍️ Feedback & Reviews System:** A dedicated review subsystem using a Java Spring Boot REST API backed by a MySQL database for community ratings and feedback.

---

## 🛠️ Technology Stack

### **Frontend**
*   **Framework:** React 18 (Vite 6, TypeScript-ready config)
*   **Styling:** Tailwind CSS v4 & custom HSL dark/light modes
*   **Routing:** React Router DOM v7 (supports dynamic routing for `/view-trip/:tripId` and `/rateus/reviews`)
*   **AI Integration:** `@google/generative-ai` & `@google/genai`
*   **Database:** Firebase Web SDK (Firestore integration)
*   **Authentication:** Google OAuth 2.0 (`@react-oauth/google`)
*   **Animations & Icons:** Lucide React, React Icons, Framer Motion

### **Backend Services**
1.  **Feedback Service (`feedbackapp`)**
    *   **Framework:** Java Spring Boot 3.5.0 (Java 21)
    *   **ORM / Database:** Spring Data JPA, Hibernate, MySQL Database
    *   **Port:** Run on port `8081`
2.  **WebSocket Chat Server (`wbsocket`)**
    *   **Framework:** Java Spring Boot 3.5.0 (Java 17)
    *   **Communication:** Spring WebSocket, STOMP Protocol, SockJS
    *   **Port:** Run on port `8080`

---

## 📂 Project Structure

```text
TravelobeSem2/
├── Backend/
│   ├── feedbackapp/            # Spring Boot REST API for Reviews & Ratings
│   │   ├── src/                # Spring Boot Java sources (MySQL JPA, Controllers, Models, Services)
│   │   └── pom.xml             # Maven dependencies (Java 21, Spring Boot 3.5.0, MySQL, Lombok)
│   └── wbsocket/               # Spring Boot WebSocket Server for instant Messaging
│       ├── src/                # Spring Boot WebSocket Controllers, Models & Configurations
│       └── pom.xml             # Maven dependencies (Java 17, Spring Boot 3.5.0, WebSocket starter)
└── Frontend/
    ├── src/                    # React Main Application Source
    │   ├── assets/             # Logos, images, and static resources
    │   ├── components/
    │   │   ├── custom/         # UI Elements: Header, Hero, and Ratings
    │   │   └── ui/             # Shadcn reusable UI components, Review Form & Review List
    │   ├── constants/          # Option configurations and AI Prompts
    │   ├── create-trip/        # Multi-step AI Travel planner configuration form
    │   ├── pages/              # Review Dashboard page
    │   ├── service/            # Global API (Google Places), AIModal (Gemini Chat), Firebase Config
    │   └── view-trip/          # Structured Itinerary details visualization page
    ├── my-app/                 # Sub-app prototype showcasing full STOMP WebSocket client chat
    ├── package.json            # React + Vite dependencies (React Router 7, Tailwind 4, Firebase)
    └── vite.config.js          # Vite build config with Tailwind 4 plugin & path aliases
```

---

## ⚙️ Getting Started & Run Instructions

Ensure you have the following installed on your system:
*   [Node.js](https://nodejs.org/) (v18+ recommended)
*   [Java Development Kit (JDK)](https://oracle.com/java/technologies/downloads/) (JDK 17 and JDK 21)
*   [Maven](https://maven.apache.org/)
*   [MySQL Server](https://www.mysql.com/)

---

### **1. Backend - Feedback Database & Service**

1.  **MySQL Database Setup:**
    Create a database named `feedback_db` in your MySQL server:
    ```sql
    CREATE DATABASE feedback_db;
    ```
2.  **Configure Environment properties:**
    Open `Backend/feedbackapp/src/main/resources/application.properties` and update the database username and password matching your local environment:
    ```properties
    spring.datasource.url=jdbc:mysql://localhost:3306/feedback_db
    spring.datasource.username=YOUR_MYSQL_USERNAME
    spring.datasource.password=YOUR_MYSQL_PASSWORD
    ```
3.  **Run the Feedback Service:**
    ```bash
    cd Backend/feedbackapp
    ./mvnw spring-boot:run
    ```
    *The service will start automatically on port `8081`.*

---

### **2. Backend - WebSocket Messaging Server**

1.  **Run the Chat Server:**
    ```bash
    cd Backend/wbsocket
    ./mvnw spring-boot:run
    ```
    *The websocket endpoint will start broadcasting on `ws://localhost:8080/ws`.*

---

### **3. Frontend - Main React Application**

1.  **Environment Setup:**
    In the `Frontend` directory, create a `.env` file to configure your credentials:
    ```env
    VITE_GOOGLE_PLACE_API_KEY=your_google_places_api_key
    VITE_GOOGLE_AUTH_CLIENT_ID=your_google_oauth_client_id.apps.googleusercontent.com
    VITE_GOOGLE_GEMINI_AI_API_KEY=your_gemini_api_key
    ```
2.  **Install & Start:**
    ```bash
    cd Frontend
    npm install
    npm run dev
    ```
    *The application will boot on `http://localhost:5173`.*

---

### **4. Frontend - WebSocket Chat Sub-App (my-app)**

1.  **Run Chat UI:**
    ```bash
    cd Frontend/my-app
    npm install
    npm run dev
    ```
    *This runs the standalone client chat interface (Chat-Club) powered by WebSockets.*

---

## 🤝 Contributing

Contributions are welcome! Please open an issue or submit a pull request with any improvements or feature updates.

