# Ouija-over-HTTPS (OoH) Technical Specification
Status: Experimental

## Abstract
This document specifies Ouija-over-HTTPS (OoH), an application layer protocol for spirit communication over HTTPS. OoH enables standardized supernatural interaction through modern web infrastructure.

## 1. Introduction
Ouija-over-HTTPS provides a standardized method for conducting spirit communication sessions over the internet. This specification defines the protocol structure, message formats, and implementation requirements for compliant OoH servers and clients.

### 1.1 Terminology

- Session: A continuous spirit communication exchange
- Medium: The server facilitating the communication
- Sitter: A client participating in the session

## 2. Protocol Overview

### 2.1 Basic Operation
OoH operates as a REST-like protocol over HTTP/HTTPS. Each session is initiated with a POST request to establish the connection with the spirit realm, followed by subsequent GET requests to receive responses and PUT requests to send queries.

### 2.2 Connection Lifecycle
1. Session Initialization
2. Participant Registration
3. Query Phase
4. Response Reception
5. Session Termination

## 3. Message Format

### 3.1 Request Format
All requests must include the following headers:
```
Content-Type: application/x-ouija
Accept: application/x-ouija
X-Ouija-Session-ID: <uuid>
X-Ouija-Sitter-Count: <integer>
```

### 3.2 Response Format
Responses are returned in json format:
```json
{
  "message": string,
  "energy_level": float
}
```

## 4. Endpoints

### 4.1 Session Management
- POST /sessions
- DELETE /sessions/{session_id}
- GET /sessions/{session_id}/status

### 4.2 Communication
- PUT /sessions/{session_id}/query
- GET /sessions/{session_id}/response
- POST /sessions/{session_id}/participants

## 5. Error Handling

### 5.1 HTTP Status Codes
- 201: Session created
- 400: Invalid request format
- 403: Insufficient sitters
- 408: Spirit connection timeout
- 429: Too many requests (spirits need some rest)
- 500: Supernatural error
- 503: Spirit realm unavailable
- 666: Demonic interference

### 5.2 Error Response Format
```json
{
  "error": string,
  "error_code": integer,
  "suggestion": string
}
```

## 6. Security Considerations

### 6.1 Transport Security
All OoH implementations must use HTTPS for transport security to prevent malicious spirit interference.

### 6.2 Authentication
Sessions must implement authentication to prevent unauthorized sitters from joining.

### 6.3 Rate Limiting
Servers must implement rate limiting to prevent spirit realm oversaturation.

## 7. Implementation Requirements

### 7.1 Server Requirements
- Must support minimum of 3 concurrent sitters
- Must maintain session state
- Must implement timeout handling

### 7.2 Client Requirements
- Must support websocket connections for real-time updates
- Must implement connection retry logic
- Must handle disconnection gracefully

## Example Session

Request:
```http
POST /sessions HTTP/1.1
Host: medium.example.com
Content-Type: application/x-ouija
X-Ouija-Sitter-Count: 3

{
  "intent": "friendly",
  "preferred_language": "en-US"
}
```

Response:
```http
HTTP/1.1 201 Created
Content-Type: application/x-ouija
X-Ouija-Session-ID: 550e8400-e29b-41d4-a716-446655440000

{
  "session_id": "550e8400-e29b-41d4-a716-446655440000",
  "status": "awaiting_spirit",
  "energy_level": 0.75
}
```
