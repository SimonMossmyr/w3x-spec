 # war3map.shd (The Shadow Map File)

This file has no header, only raw data.

Size of the file = (16\*map_width\*map_height) bytes

1byte can have 2 values:<br>
`00h` = no shadow<br>
`FFh` = shadow

Each byte set the shadow status of 1/16 of a tileset. It means that each tileset is divided in 16 parts (4\*4).
