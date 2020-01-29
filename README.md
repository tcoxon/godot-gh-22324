This is a reproducer for Godot issue #22324. https://github.com/godotengine/godot/issues/22324

To reproduce the issue:
1. Clone the project
2. Open the project in Godot 3.1 or 3.2
3. Without editing anything, run the main scene (Test.tscn), and just close the window when it appears
4. In a terminal run `git status` and observe the changes to Test.tscn.

Tested in Godot 3.1 (Windows and Linux) and 3.2 (Linux)

The diff looks something like this:

```
diff --git a/Test.tscn b/Test.tscn
index a9a0e1b..6b151d1 100644
--- a/Test.tscn
+++ b/Test.tscn
@@ -7,7 +7,7 @@
 [node name="GridMap" type="GridMap" parent="."]
 mesh_library = ExtResource( 1 )
 data = {
-"cells": PoolIntArray( 0, 0, -1610612736, 1, 0, -1610612735, 2, 0, -1610612735, 65535, 0, 0, 0, 1, 1, 1, 1, -2147483647, 65535, 1, 1610612736, 2, 65535, 536870913 )
+"cells": PoolIntArray( 0, 0, 536870912, 1, 0, 1, 2, 0, -1610612735, 65535, 0, -1610612736, 0, 1, -1610612735, 1, 1, 536870913, 65535, 1, 536870912, 2, 65535, 1 )
 }
 __meta__ = {
 "_editor_clip_": 0
```

Uninitialised memory in the gaps in the gridmap?
