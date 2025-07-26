# Websocket Chat Application 
A real-time, one-to-one chat application built using Spring Boot for the backend and plain JavaScript with WebSockets for the frontend. This project demonstrates how to use WebSockets to create interactive and live user experiences.

## Features
* User Authentication: Simple user login using a nickname and full name.
* Real-Time User Presence: See a list of all connected users in real-time. The application instantly updates when users connect or disconnect.
* One-to-One Private Messaging: Click on a user from the list to start a private chat session.
* Chat History: Loads the previous conversation history when you select a user to chat with.
* Live Message Updates: Messages are sent and received instantly without needing to refresh the page, using STOMP over WebSockets.
* Unread Message Indicators: (Although the functionality seems partial in the code) The UI is set up to show notifications for new messages from users you are not actively chatting with.

## Technologies Used
This project is built with a combination of backend and frontend technologies:

### Backend:
* Java 17
* Spring Boot 3
* Spring WebSocket: For handling WebSocket connections and messaging.
* STOMP (Streaming Text Oriented Messaging Protocol): As the sub-protocol for WebSocket communication.
* Maven: For project dependency management.

### Frontend:
* HTML5
* CSS3
* JavaScript (ES6+): For all client-side logic.
* SockJS: A browser JavaScript library that provides a WebSocket-like object. It's a fallback for environments that don't support WebSockets.
* Stomp.js: A client library for using the STOMP protocol over WebSockets.


## Getting Started
Follow these instructions to get a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites
Make sure you have the following software installed on your machine:
* Java Development Kit (JDK) - Version 17 or later.
* Apache Maven - To build the project and manage dependencies.
* A modern web browser (e.g., Chrome, Firefox, Edge).

### Installation & Setup
1. __Clone the repository__:
   ```bash
   git clone https://github.com/Robwert0/Websocket_Chat.git
   cd Websocket_Chat
   ```

2. **Run the Backend (Spring Boot Application)**:
   
   
   You can run the Java server in one of two ways:
  
   * **Using Maven**:
    
     Open a terminal in the root of the project directory and run the following command:
     ```bash
     mvn spring-boot:run
     ```
   * **Using an IDE (IntelliJ IDEA, Eclipse, etc.)**:
    
     Import the project as a Maven project and run the main application class: `com.name.ChatappApplication`.
    
     The backend server will start on `http://localhost:8088`.

3. **Access the Frontend Application**:

   Once the backend server is running, you can access the chat application:
  
   1. Open your web browser.
   2. Navigate to http://localhost:8088.
   3. You will see the login page. Enter a nickname and a full name to join the chat.
   4. To test the real-time functionality, open a second browser window (or an incognito window) and log in as a different user.

## How It Works
The application follows a client-server architecture.

1. The Spring Boot backend acts as the WebSocket server. It manages user connections, disconnections, and routes messages between clients using a message broker.
2. The `/app` destination prefix is used for messages bound for methods annotated with `@MessageMapping`.
3. The `/user` destination prefix is used for sending private messages to specific users.
4. The frontend client uses `SockJS` and `Stomp.js` to connect to the server's WebSocket endpoint (`/ws`).
5. When a user logs in, they subscribe to their unique message queue (`/user/{nickname}/queue/messages`) to receive private messages.
6. When a user sends a message to another user, the message is sent to the server, which then forwards it to the recipient's message queue. The application updates the UI dynamically upon receiving a message.
