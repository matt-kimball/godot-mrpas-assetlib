# GDScript MRPAS

Mingos' Restrictive Precise Angle Shadowcasting (MRPAS) is an algorithm
used by traditional roguelike games for determining which map cells
are in the player's field of view.  This project implements that algorithm
in GDScript (for use in the Godot game engine).

![screenshot](screenshot.png)

For a description of the algorithm, see
[the overview on RogueBasin](http://www.roguebasin.com/index.php?title=Restrictive_Precise_Angle_Shadowcasting).

[A live web build of this project can be found on itch.io.](https://mkimball.itch.io/godot-mrpas-demo)

Source code for the demo project is [available on github](https://github.com/matt-kimball/godot-mrpas).

# Usage

To use this implementation, one can simply drop `mrpas.gd` into an existing
Godot project.

Expected usage is as follows:

```
    # Create algorithm instance with a particular map size.
    var mrpas = MRPAS.new(map_size)

    # Mark some positions in the map as occluders.  Here we do this once,
    # but it should be done for every non-transparent map cell. 
    mrpas.set_transparent(occluder_position, false)

    # Mark all cells as non-visible.  Necessary if the MRPAS object is
    # reused for multiple computations.
    mrpas.clear_field_of_view()

    # Compute which map cells are visible from the view position.
    mrpas.compute_field_of_view(view_position, max_view_distance)

    # Now that the field of view has been computed, we can check individual
    # map cells to see if they are visible from the view position.
    if mrpas.is_in_view(map_cell_position):
        ...  # Perform some action here when the cell is in view.
```

# License

This implementation is available under the MIT License.
