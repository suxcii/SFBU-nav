SFBU NAV - INDOOR NAVIGATION - HOW TO RUN
==============================================

What's in this folder
---------------------
index.html   the app (3D map, 2 floors, search, 360 photos)
server.py    the AI search (runs on the DGX, use later)
photos/      sample 360 photos (replace with your real ones)

How to open it on your laptop
-----------------------------
The 360 photos only load through a small local web server
(opening index.html by double-click shows the map, but photos won't load).

1. Install Python if you don't have it (python.org).
2. Open a terminal / command prompt IN THIS FOLDER.
3. Run:      python -m http.server 5500
4. Open Chrome and go to:   http://localhost:5500

Try it
------
- Click 1F / 2F / All to switch floors, 2D / 3D to change the view.
- Type "print" or "tuition" in the search box.
- Click an orange camera icon -> you fade into the 360 photo.
- Click the arrows inside the photo to walk to the next photo.
- "Back to map" (or Esc) returns to the 3D map.

Mascot = where you are
----------------------
- Drag the mascot with the mouse to move it on the floor you are viewing.
- Double-click anywhere on a floor to put the mascot there
  (switch to 2F first, then double-click, to move it to the 2nd floor).
- Search for a room: glowing dots show the route, plus left/right and distance.
- Words like "wheelchair" or "elevator" make the route use the elevator.
- After a search the mascot walks the route (up the stairs too) and says when it arrives.
  Dragging the mascot, a new search, or Reset stops the walk.
- Reset puts the mascot back at the entrance.

Use your own school
-------------------
1. Rooms:  edit the BUILDING list near the top of index.html
           (x, z, w, d = squares on your grid drawing).
2. Photos: use the phone's normal Panorama mode (PHOTO_MODE = 'panorama').
           Start facing the TOP of your paper, turn LEFT -> RIGHT a full circle.
           Didn't turn a full circle? add  sweep: 270  (degrees turned) to that photo.
           Put the photos in the photos folder, then edit the
           PHOTOS list: file name, floor, x, z where you stood,
           and which way the phone faced when you started ("top" of paper).
3. Arrows between photos are made automatically.
   If an arrow points the wrong way, add  yawFix: 90  (or -90 / 180) to that photo.

Turn on the AI search (on the DGX)
----------------------------------
   ollama pull llama3.1:8b
   pip install fastapi uvicorn requests
   uvicorn server:app --host 0.0.0.0 --port 8000
Then in index.html change   const USE_AI = false;   to   true
