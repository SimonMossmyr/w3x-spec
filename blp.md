# "war3mapMap.blp" the minimap image (with the help of BlacKDicK)

The BLP file contain the JPEG header and the JPEG raw data separated. BLP stands for "Blip" file which I guess is a "BLIzzard Picture".

There are two types of BLPs:
- JPG-BLPs:�use JPG compression
- Paletted BLPs: use palettes and 1 or 2 bytes per pixel depending

## File format
### Header
| Size | Description |
|----|---------|
| `char[4]` | file ID ("BLP1") |
| `int` | 0 for JPG-BLP, 1 for Paletted |
| `int` | 0x00000008 = has alpha, 0x00000000 = no alpha |
| `int` | image width |
| `int` | image height |
| `int` | flag for alpha channel and team colors (usually 3, 4 or 5), 3 and 4 means color and alpha information for paletted files, 5 means only color information, if >=5 on 'unit' textures, it won't show the team color. |
| `int` | always 0x00000001, if 0x00000000 the model that uses this texture will be messy. |
| `int[16]` | mipmap offset (offset from the begining of the file) |
| `int[16]` | mipmap size (size of mipmaps) |

### JPG-BLP
| Size | Description |
|----|---------|
| `int` | jpg header size (header size) "h" (usually 0x00000270) |
| `byte[h]` header |

followed by 0 bytes until the begining of the jpeg data, we can safely erase these 0 bytes if we fix the mipmap offset specified above

| Size | Description |
|----|---------|
| `byte[16, mipmap size]` | starting from each of the 16 mipmap offset addresses we read 'mipmap size' bytes raw jpeg data till the end of the file, having the header and the mipmap data we can process the picture like ordinary JPG files |

### BLP
| Size | Description |
|----|---------|
| `byte[4, 255]` | the BGRA palette defining 256 colors by their BGRA values, each 1 byte |
| `byte[width x height]` | the ColorIndex of each pixel from top left to bottom right, ColorIndex refers to the above defined color palette |
| `byte[width x height]` | the AlphaIndex of each pixel on a standard greyscale palette for the alpha channel, where 0 is fully transparent and 255 is opaque, if the picturetype flag is set to 5, the image doesn't have an alpha channel, so this section will be omitted |

More detailed blp specs by Magos: http://magos.thejefffiles.com/War3ModelEditor/
