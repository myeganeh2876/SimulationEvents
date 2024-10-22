# Unity Client Events Documentation

## Overview
This documentation outlines the events a hosting client can utilize when interfacing with Unity. These events are dispatched when changes occur within the Unity application, allowing the hosting client to respond accordingly.

## Event List

### **1. Initialized Event**
Recieved when unity splash screen in shown and app is ready to accept events
```json
{
  "message": "initialized"
}
```
---

### **2. View Transition Event**
Recieved whenever something is moving, all overlays must be hidden when transition starts and redrawn when transition ends
```json
{
  "context": "Office",
  "contextData": {
    "type": "ViewTransition",
    "data": {
      "transitionState": "After",
      "from": "<From View>",
      "to": "<To View>"
    }
  }
}
```

---

### **3. Workspace View Drag Change Event**
The behaviour of overlays should be like entering a transition, except the key are different you hide the overlays when stateType is `"Enter"` and show the overlays when stateType is `"Exit"`
```json
{
  "context": "Office",
  "contextData": {
    "type": "WorkspaceViewDragChange",
    "data": {
      "stateType": "Enter"
    }
  }
}
```
---

### **4. Room Event**
Recieved when a room is focused or created
```json
{
  "context": "Office",
  "contextData": {
    "type": "Room",
    "data": {
      "roomId": "<Room ID>",
      "timelineBoardScreenSpaceLocation": {...},
      "chartBoardScreenSpaceLocation": {...}
    }
  }
}
```

#### Behavior:
- Updates the timeline and chart board corners for a specific room.
- Identifies and handles room-specific data within a building.

---

### **5. Building Event**
Recieved when a building is focused or created
```json
{
  "context": "Office",
  "contextData": {
    "type": "Building",
    "data": {
      "buildingId": "<Building ID>",
      "roomPositions": [{...}],
      "wallCorners": [{...}],
      "rootRoomPosition": {...}
    }
  }
}
```

#### Behavior:
- Updates wall corners and room positions for a specific building.
- Handles data related to building layout and rooms within it.

---

### **6. Workspace Event**
Recieved when user goes to land view
```json
{
  "context": "Office",
  "contextData": {
    "type": "Workspace",
    "data": {
      "buildingPositions": [{...}]
    }
  }
}
```

#### Behavior:
- Updates the positions of buildings on the workspace.

---

### **7. Board Event**
Recieved when either of the boards in a room is clicked
```json
{
  "context": "Office",
  "contextData": {
    "type": "Board",
    "data": {
      "roomId": "<Room ID>",
      "board": "Chart"
    }
  }
}
```

#### Behavior:
- Handles interactions with a chart or timeline board within a room.

---

### **8. Character Location Event**
Recieved when a character moves, there is a different event like this for each of the characters in a room
```json
{
  "context": "Office",
  "contextData": {
    "type": "CharacterLocation",
    "data": {
      "associatedRoomId": "<Room ID>",
      "screenSpacePosition": {
        "x": 0,
        "y": 0
      }
    }
  }
}
```

#### Behavior:
- Tracks character positions within rooms based on screen space coordinates.

---

### **9. BuildingPlus Event**
Recieved when the + button on the top left of the floor is clicked
```json
{
  "context": "Office",
  "contextData": {
    "type": "BuildingPlus",
    "data": {
      "buildingId": "<Building ID>",
      "level": 0
    }
  }
}
```

#### Behavior:
- triggers a goal popup when goals are available for the selected level.
