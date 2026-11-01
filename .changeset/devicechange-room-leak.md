---
'livekit-client': patch
---

Fix a memory leak where a `Room` was never garbage collected after the application dropped it. The `devicechange` listener on `navigator.mediaDevices` and the `FinalizationRegistry` cleanup callback both held the `Room` through the constructor's closure context, so the registry callback never ran and every `Room` stayed in memory with its engine and peer connections.
