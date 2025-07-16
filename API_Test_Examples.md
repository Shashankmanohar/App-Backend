# Tricksy Backend API Test Examples (Full)

Below are example requests and sample values for testing all backend API routes. For protected routes, include the header:

```
Authorization: Bearer <token>
```

---

## Admin  

### Login
```
POST /api/admin/login
{
  "email": "admin@tricksy.com",
  "password": "admin123"
}
```
**Response:**
```
{
  "message": "Admin login successful",
  "token": "<jwt>",
  "admin": { "_id": "...", "name": "Admin", "email": "admin@tricksy.com", "phone": "1234567890" }
}
```

### Get Profile
```
GET /api/admin/profile
Headers: Authorization: Bearer <token>
```

### Get All Admins
```
GET /api/admin/all-admins
Headers: Authorization: Bearer <token>
```

### Get Total Users/Drivers/Today's Attendance
```
GET /api/admin/total-users
GET /api/admin/total-drivers
GET /api/admin/todays-attendance
Headers: Authorization: Bearer <token>
```

### Register User/Driver
```
POST /api/admin/register-user
Headers: Authorization: Bearer <token>
{
  "name": "User One",
  "email": "user1@tricksy.com",
  "phone": "1234567890",
  "address": "123 Main St",
  "password": "user123"
}

POST /api/admin/register-driver
Headers: Authorization: Bearer <token>
{
  "name": "Driver One",
  "email": "driver1@tricksy.com",
  "phone": "9876543210",
  "address": "456 Main St",
  "password": "driver123",
  "busNumber": "BUS-101"
}
```

### Get All Users/Drivers
```
GET /api/admin/all-users
GET /api/admin/all-drivers
Headers: Authorization: Bearer <token>
```

### Delete User/Driver
```
DELETE /api/admin/user/<userId>
DELETE /api/admin/driver/<driverId>
Headers: Authorization: Bearer <token>
```

---

## User

### Login
```
POST /api/user/login
{
  "email": "user1@tricksy.com",
  "password": "user123"
}
```

### Get/Update Profile
```
GET /api/user/profile
PATCH /api/user/profile
Headers: Authorization: Bearer <token>
{
  "name": "User One Updated",
  "phone": "1112223333"
}
```

---

## Driver

### Login
```
POST /api/driver/login
{
  "email": "driver1@tricksy.com",
  "password": "driver123"
}
```

### Get Profile
```
GET /api/driver/profile
Headers: Authorization: Bearer <token>
```

---

## Accommodation

### Create Accommodation (User)
```
POST /api/accommodation/create
Headers: Authorization: Bearer <token>
Content-Type: multipart/form-data
Fields:
  title: "Need Room"
  message: "Looking for a single room."
  images: (file upload)
  videos: (file upload)
```

### Get User Accommodations
```
GET /api/accommodation/user
Headers: Authorization: Bearer <token>
```

### Get Accommodation by ID
```
GET /api/accommodation/<accommodationId>
Headers: Authorization: Bearer <token>
```

### Admin: Get All, Update, Delete
```
GET /api/accommodation/admin/all
PUT /api/accommodation/admin/<accommodationId>
DELETE /api/accommodation/admin/<accommodationId>
Headers: Authorization: Bearer <admin token>
Body for PUT:
{
  "status": "approved",
  "adminResponse": "Approved for next week."
}
```

---

## Attendance

### Mark Attendance (User/Driver)
```
POST /api/attendance/mark
Headers: Authorization: Bearer <token>
{
  "notes": "Arrived on time",
  "location": "123 Main St",
  "status": "present"
}
```

### Check Out (User/Driver)
```
POST /api/attendance/checkout
Headers: Authorization: Bearer <token>
{
  "notes": "Leaving early"
}
```

### Get User Attendance
```
GET /api/attendance/user
Headers: Authorization: Bearer <token>
Optional query: ?startDate=2024-06-01&endDate=2024-06-10
```

### Admin: Get All, Update Status, Stats
```
GET /api/attendance/admin/all
PUT /api/attendance/admin/<attendanceId>
GET /api/attendance/admin/stats
Headers: Authorization: Bearer <admin token>
Body for PUT:
{
  "status": "present",
  "notes": "Corrected status"
}
```

---

## Leave

### Apply for Leave (User/Driver)
```
POST /api/leaves/apply
Headers: Authorization: Bearer <token>
{
  "startDate": "2024-06-01",
  "endDate": "2024-06-03",
  "reason": "Medical"
}
```

### Get My Leaves
```
GET /api/leaves/my
Headers: Authorization: Bearer <token>
```

### Get All Leaves (Admin/User)
```
GET /api/leaves/
Headers: Authorization: Bearer <token>
```

### Update Leave Status (Admin)
```
PATCH /api/leaves/<leaveId>/status
Headers: Authorization: Bearer <admin token>
{
  "status": "approved",
  "adminResponse": "Approved for medical leave."
}
```

### Get Leaves by Status
```
GET /api/leaves/status/<status>
Headers: Authorization: Bearer <token>
```

---

## Driver Location

### Update Driver Location
```
POST /api/driver-location/update
Headers: Authorization: Bearer <driver token>
{
  "latitude": 28.6139,
  "longitude": 77.2090,
  "accuracy": 5,
  "speed": 40,
  "heading": 90
}
```

### Set Driver Offline
```
POST /api/driver-location/offline
Headers: Authorization: Bearer <driver token>
```

### Get All Driver Locations (Admin)
```
GET /api/driver-location/all
Headers: Authorization: Bearer <admin token>
```

### Get Driver Location by ID (Admin)
```
GET /api/driver-location/driver/<driverId>
Headers: Authorization: Bearer <admin token>
```

---

## Driver Assignment

### Assign Driver to Users (Admin)
```
POST /api/driver-assignment/assign
Headers: Authorization: Bearer <admin token>
{
  "driverId": "<driverId>",
  "userIds": ["<userId1>", "<userId2>"],
  "pickupLocation": "Hostel Gate",
  "dropLocation": "Main Campus",
  "pickupCoordinates": { "latitude": 28.6139, "longitude": 77.2090 },
  "dropCoordinates": { "latitude": 28.7041, "longitude": 77.1025 },
  "notes": "Morning pickup"
}
```

### Get All Assignments (Admin)
```
GET /api/driver-assignment/all
Headers: Authorization: Bearer <admin token>
```

### Update Assignment Status (Admin)
```
PATCH /api/driver-assignment/<assignmentId>/status
Headers: Authorization: Bearer <admin token>
{
  "status": "completed"
}
```

### Delete Assignment (Admin)
```
DELETE /api/driver-assignment/<assignmentId>
Headers: Authorization: Bearer <admin token>
```

### Get Driver Assignments (Driver)
```
GET /api/driver-assignment/driver/<driverId>
Headers: Authorization: Bearer <driver token>
```

### Update User Status in Assignment (Driver)
```
PATCH /api/driver-assignment/<assignmentId>/user-status
Headers: Authorization: Bearer <driver token>
{
  "userId": "<userId>",
  "status": "picked" // or "dropped"
}
```

### Get User Assignment (User)
```
GET /api/driver-assignment/user
Headers: Authorization: Bearer <user token>
```

### Get Assigned Driver Location (User)
```
GET /api/driver-assignment/user/driver-location
Headers: Authorization: Bearer <user token>
```

---

> For all protected routes, always include the `Authorization: Bearer <token>` header after logging in as the appropriate user, admin, or driver. Replace placeholder IDs and tokens with actual values from your database and login responses. 